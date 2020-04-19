# 3.6 Estruturas de Repetição

Para realizar um *looping* dentro de uma lista, existem algumas formas interessantes de se fazer isso.

O mais comum nas linguagens em geral é a estrutura do `for`, que também existe dentro do elixir, porém não é a mais utilizada.

```elixir
iex> for x <- [1, 2, 3] do
...>   x + 2
...> end
[3, 4, 5]
```

No exemplo acima, criamos uma repetição dentro da lista de números o qual cada elemento iterado fora definido o valor na variável x e dentro dessa estrutura, x foi somado com 2 retornando uma nova lista de números modificada.

Mas essa não é a forma mais comum de se fazer um looping, pois em suma, utilizamos o módulo `Enum` para gerenciar Enumeradores em geral.

Por exemplo, se queremos somar o valor total de um carrinho de um e-commerce, seguimos essa lógica:

```elixir
iex> lista_carrinho = [ \
...>   %{valor_unitario: 125, quantidade: 2, valor_total: 250}, \
...>   %{valor_unitario: 9210, quantidade: 1, valor_total: 9210}, \
...>   %{valor_unitario: 1000, quantidade: 20, valor_total: 20000} \
...> ]
[
  %{quantidade: 2, valor_total: 250, valor_unitario: 125},
  %{quantidade: 1, valor_total: 9210, valor_unitario: 9210},
  %{quantidade: 20, valor_total: 20000, valor_unitario: 1000}
]

iex> valor_total = Enum.reduce(lista_carrinho, 0, fn item, valor_a_somar ->
...>   valor_a_somar + item.valor_total
...> end)
29460
```

### Enumeradores

Dentro desse maravilhoso módulo, podemos realizar inúmeras operações tanto com listas, tanto com estruturas (*Structs*). Um exemplo legal é quando você precisa iterar dentro de uma struct para alterar as chaves de String para Átomo:

```elixir
iex> estrutura = %{"id" => 123, "nome" => "aleDsz"}
%{"id" => 123, "nome" => "aleDsz"}

iex> estrutura |> Enum.map(fn {chave, valor} ->
...>   {String.to_atom(chave), valor}
...> end)
[id: 123, nome: "aleDsz"]
```

Porém, podemos ver que ao fazer isso, o retorno é uma lista de palavras chave (Keyword List), que nada mais é uma lista com chave e valor, assim como uma estrutura, porém funciona um pouco diferente.

Só que, como nós queríamos alterar de String para Átomo, é necessário definir após a execução, na qual é necessário enviar a resposta para a função de `Enum.into/2`, passando como primeiro argumento a lista de palavras chave e como segundo argumento, uma struct vazia.

```elixir
iex> estrutura = %{"id" => 123, "nome" => "aleDsz"}
%{"id" => 123, "nome" => "aleDsz"}

iex> estrutura |> Enum.map(fn {chave, valor} ->
...>   {String.to_atom(chave), valor}
...> end) |> Enum.into(%{})
%{id: 123, nome: "aleDsz"}
```

Acima há apenas exemplos de uso, mas para que isso fique bem claro, iremos definir melhor como funciona cada forma de loop com o módulo de `Enum`.

##### Enum.map

Essa função executa o que o próprio nome diz, ele mapeia todos os itens dentro de um Enumerador retornando a mesma quantidade de elementos, porém estes elementos podem ter sido alterados.

Um bom exemplo, é o mesmo utilizado na estrutura do `for`, porém utilizando o módulo de `Enum`.

```elixir
iex> Enum.map([1, 2, 3], fn x ->
...>   x + 2
...> end)
[3, 4, 5]
```

##### Enum.reduce

Quando precisamos pegar uma lista de reduzí-la (ou aumentá-la, depende do contexto) para algum formato, seja este de tamanho diferente do original, precisamos utilizar o conceito da função `Enum.reduce/3`, que precisa de 3 argumentos:

  1) Enumerador;
  2) Valor inicial;
  3) Função anônima pra execução do looping

Tendo isso em mente, podemos analisar melhor o exemplo citado anteriormente da soma dos itens do carrinho do e-commerce.

##### Enum.reduce_while

Utiliza-se o mesmo conceito do `Enum.reduce/3`, apenas com uma diferença: É possível parar o looping no meio de sua execução se definido o resultado do looping como uma tupla, obedecendo as duas formas de resposta:

- `{:cont, acumulador}`: Este define que o looping deve continuar, o acumulador para o próximo passo do looping com o valor novo

- `{:halt, resultado}`: Geralmente utilizando para ou retornar um erro, ou apenas encerrar o looping devolvendo o resultado do mesmo até o último laço executado.

```elixir
iex> Enum.reduce_while(1..100, 0, fn numero, soma ->
...>   cond do
...>     numero == 10 ->
...>       {:cont, soma + numero}
...> 
...>     numero == 40 ->
...>       {:cont, soma + numero}
...> 
...>     soma >= 60 ->
...>       {:halt, soma}
...> 
...>     true ->
...>       {:cont, soma + 1}
...>   end
...> end)
88
```