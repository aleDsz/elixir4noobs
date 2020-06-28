# 3.6 Módulos

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

Dentro e/ou fora dos módulos é possível que você inclua-os dentro do seu código para a execução de funções dentro dos mesmos.

Existem 4 formas de se fazer isso:

 - **alias**
 - **import**
 - **require**
 - **use** ([metaprogramação](https://elixirschool.com/pt/lessons/advanced/metaprogramming/))

### Alias

Quando realizamos uma *alias*, estamos definindo um "apelido" ao módulo para ser utilizado dentro do nosso contexto (sendo ele um módulo ou um script [.exs]):

```elixir
defmodule MyApp.A do
  def funcao() do
    1 + 1
  end
end

defmodule MyApp.B do
  alias MyApp.A

  def funcao() do
    A.funcao() # 2
  end
end
```

### Import

Já no import, utilizando esse para literalmente importar todas as funções de um módulo para outro como se fossem funções do próprio módulo:

```elixir
defmodule MyApp.A do
  def funcao() do
    1 + 1
  end

  def funcao2() do
    1 + 1
  end
end

defmodule MyApp.B do
  import MyApp.A

  def funcao3() do
    funcao() + funcao2() # 4
  end
end
```

**Curiosidade:** Você pode importar funções específicas de um módulo apenas para o mesmo não demore para ser compilado defivo à tantas funções dentro do módulo `MyApp.A`:

```elixir
defmodule MyApp.A do
  def funcao() do
    1 + 1
  end

  def funcao2() do
    1 + 1
  end

  def funcao3() do
    1 + 1
  end

  def funcao4(a, b, c, d \\ 0) do
    1 + 1
  end
   
   # ...
end

defmodule MyApp.B do
  import MyApp.A, only: [funcao1: 0, funcao2: 0]

  def funcao3() do
    funcao() + funcao2() # 4
  end
end
```

**Curiosidade 2:** Você também pode apenas importar uma mesma função porém com o tamanho específico de argumentos.  Ou seja, por conta do *pattern matching* e de argumentos opcionais, é possível que uma mesma função do mesmo nome exista mais de uma vez dentro do contexto do Módulo.

Isso quer dizer que, `funcao4/3` e `funcao4/4` é a mesma função porém uma com apenas 3 argumentos e uma com 4 argumentos, visto que o 4º argumento é opcional pois ele tem já um valor pré-definido como `0`.

### Require

Devido ao uso de metaprogramação, é possível executar Macros diretamente de um módulo quando utilizamos o "requerimento" de outro módulo. Um exemplo é o módulo de logs do Elixir, que só é possível usar quando executamos o require dele:

```elixir
iex> Logger.info("Test")
** (CompileError) iex:1: you must require Logger before invoking the macro Logger.info/1
    (elixir) src/elixir_dispatch.erl:97: :elixir_dispatch.dispatch_require/6

iex> require Logger
Logger

iex> Logger.info("Test")
03:39:21.479 [info]  Test
:ok
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