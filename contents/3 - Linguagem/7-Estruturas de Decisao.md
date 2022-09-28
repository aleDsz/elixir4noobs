# 3.7 Estruturas de Decisão

Quando precisamos tomar decisões difíceis e complicadas em nosso código, é sempre bom utilizar uma das estuturas de decisão.

No Elixir, estes foram criados para serem utilizados dentro de contextos com a devida semântica. Ou seja, pode-se dizer que existem estruturas de decisões que fazem a mesma coisa, só tem uma forma diferente de se entender por sua escrita.

### IF

O famoso if continua existindo no Elixir assim como em todas as outras, mas o que diferencia é que não é possível realizar vários `else if`, ou seja, você na verdade precisa criar um bloco de `if` dentro da definição do `else`:

```elixir
defmodule Decisao do
  def esta_decidido?() do
    if 1 == 2 do
      true
    else
      if 1 == 3 do
        true
      else
        if 1 == 1 do
          true
        else
          false
        end
      end
    end
  end
end
```

### Unless

A não ser que, você esteja atrás de uma semântica interessante, você deve utilizar essa estrutura.

Brincadeiras à parte, essa estrutura de decisão é exatamente o que o nome diz, uma validação ao contrário. Ou seja, caso a definição da condição tenha como resultado um booleano `true`, o bloco de código definido será executado:

```elixir
iex> hit_or_miss? = false
iex> unless hit_or_miss? === true do
...>    IO.puts "Sim, eu sou o diferentão"
...>    IO.puts "A não ser que você esteja errado ;)"
...> end
"Sim, eu sou o diferentão"
"A não ser que você esteja errado ;)"
```

### Case

Quando precisamos analisar inúmeras possíveis respostas de uma função, a estrutura de `case` é a melhor por conta de ser a mais simples e ter uma semântica mais `clean` para tal:

```elixir
iex> case AqueleModulo.com_uma_resposta_muito_doida() do
...>   "resposta 1" ->
...>     "que loucura bicho"
...> 
...>   :atomo_muito_loco ->
...>     "que loucura bicho"
...> 
...>   %{name: "Desestruct memo"} ->
...>     "que loucura bicho"
...> 
...>   _qualquer_outra_resposta_mirabolante ->
...>     "ai tu cagou tudo mermão"
...> end
```

### Cond

Não é o Conde Drácula, mas esse aqui serve pra quando você precisa validar várias condições sem a necessidade de `if .. else .. if .. else`, etc.

```elixir
iex> cond do
...>   1 == 2 ->
...>     "esse aqui é utopia, igual ancap"
...> 
...>   1 == 3 ->
...>     "esse aqui é utopia, igual ancap"
...> 
...>   1 == 4 ->
...>     "esse aqui é utopia, igual ancap"
...> 
...>   1 == 0 ->
...>     "esse aqui é utopia, igual ancap"
...> 
...>   true ->
...>     "acho que não teve jeito mesmo"
...> end
```

### With

Podia ser um `with` ela (ou ele, ou elu), mas é só uma função do `Kernel` para avaliar uma ou mais condições, é recomendado utilizar em momentos que seu `case` começar a ficar aninhado.

Dado uma função, se o seu retorno for o esperado (para isso sera utilizado o [pattern matching](../4%20-%20Recursos%20extras/3-Pattern%20Matching.md)), execute o código. Ficará mais fácil entender com o exemplo a seguir:

```elixir
iex> with {:ok, _banana} <- MyModule.my_fun(my_param) do
...>  "Deu boa patrão"
...> end
```

Basicamente, se a função retornar uma tupla de `{:ok, qualquer_valor}` (valores que você pode definir como quiser), o trecho de código no bloco `do` será executado. Caso contrario, um erro é retornado para quem chamou a função.

O `with` pode receber várias condições para avaliar, e também pode conter um bloco de `else` para tratar qualquer cláusula que não seja esperada no bloco `with ... do`. Para tratar tais cláusulas você pode usar uma espécie de `case`.

```elixir
iex> with {:ok, _banana} <- MyModule.my_fun(my_param),
...>      _another_banana <- MyModule.my_other_fun(my_param) do
...>  "Deu boa patrão"
...> else
...>  :error -> 
...>    "Deu merda patrão"
...>
...>  _other_error ->
...>    "Deu outra merda patrão"
...> end
```

Também é possível capturar os valores esperados utilizando o operador de atribuição.

```elixir
iex> with %Struct{} = struct <- MyModule.my_fun(my_param) do
...>  "Capturado chefia, #{struct}" 
...> end
```