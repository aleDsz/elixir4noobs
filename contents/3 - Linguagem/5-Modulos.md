# 3.5 Módulos

Dentro de uma aplicação feita em Elixir, para que você tenha acesso à um conjunto de funções descritas dentro de um arquivo, utiliza-se **Módulos** para que, quando compilado, você não precise carregar um arquivo parar executar uma função.

Então, você define um módulo o qual pode conter dentro:

 - uma Struct (como explicado na lição anterior);
 - funções;
 - uma [Macro](https://elixirschool.com/pt/lessons/advanced/metaprogramming/) (metaprogramação);
 - um [Guard](https://elixirschool.com/pt/lessons/basics/functions/#guards) (`pattern matching`);
 - um [Protocolo](https://elixirschool.com/pt/lessons/advanced/protocols/).

```elixir
defmodule Modulo do
  # Hello darkness, my old friend...
end
```

## Funções

Assim como outras linguagens, você pode definir funções (e não métodos) para execução de dos passos a serem seguidos para o tratamento do dado recibido por tal. Você também pode definir funções privadas e públicas.

```elixir
defmodule Modulo do
  def minha_funcao_publica() do
    1 + minha_funcao_privada()
  end

  defp minha_funcao_privada() do
    1
  end
end
```

No exemplo acima, colocamos uma função pública que chama a função privada para a execução do código. Isso é um bom exemplo do que conversamos anteriormente sobre o paradigma funcional.

Você, por padrão, apenas deixa funções públicas as quais serão chamadas por outros módulos, e deixa funções privadas dentro de um módulo quando seguimos um passo-a-passo para o processamento de um dado até que se torne uma informação na hora de retornar isso para a outro ponta (seja ela uma API, um serviço, etc.).

**Curiosidade:** Os nomes de funções são em **snake_case** e o nome dos módulos sempre em maiúsculo, ou o interpretador não entenderá o mesmo como um módulo.

A não ser que você defina a referencia de um módulo em uma variável. Exemplo:

```elixir
iex> defmodule A do
...>   def executar(x) do
...>     x * 2
...>   end
...> end
iex> x = A
iex> x.executar(2)
4
```

### Funções anônimas

No Elixir também é possível criar funções privadas dentro do mesmo contexto, podendo ser repassada para outros contextos por meio dos parâmetros das funções:

```elixir
iex> funcao = (fn x ->
...>   x * 30
...> end)
#Function<20.128620087/0 in :erl_eval.expr/5>
iex> funcao2 = (fn func ->
...>   func.(10)
...> end)
#Function<20.128620087/0 in :erl_eval.expr/5>
iex> funcao2.(funcao)
300
```