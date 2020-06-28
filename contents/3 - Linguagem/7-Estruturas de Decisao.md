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