## 3.4 - Variáveis

Como dito anteriormente no curso, as variáveis não se comportam como variáveis na maioria dos casos.

Ou seja, se você apenas está definindo uma variável com um valor numérico e posteiormente você apenas altera essa variável no mesmo contexto, a mesma terá um valor novo.

```elixir
iex> x = 10
10

iex> x = 20
20
```

**Curiosidade:** No paradigma funcional, as "variáveis" se comportam como constantes, já que a mesma não varia por conta da imutabilidade.

## Tipos

Assim como em outras linguagens de programação, no Elixir nós temos vários tipos de variáveis, porém a linguagem não é fortemente tipada como Java, C# e outras.

Você tem a liberdade de trabalhar sem definir tipos às contantes, porém isso te deixa menos inseguro do que você irá receber ou devolver em uma função, e não precisa definir um tipo na hora de declarar a mesma.

```elixir
nome = "Alexandre"
idade = 23
maior_de_idade? = true
```

**Curiosidade:** Você pode utilizar símbolos como `?` e `!` na hora de definir variáveis ou nome de funções.

Quando definido que uma variável ou função contém o símbolo de interrogação (?) no final da mesma, entende-se que o resultado daquela variável ou função será um booleano.

Quando definido que uma função contém o símbolo de exclamação (!) no final da mesma, entende-se que o resultado será um valor ou uma `exception`.

Mas vamos direto ao assunto, existem vários tipos no Elixir, tais como:

```elixir
# Átomos (Atom)
iex> :atomo
:atomo

# String (Binary)
iex> "Esta é uma string maravilhosa"
"Esta é uma string maravilhosa"

# Booleano (Boolean)
iex> true
true

# Inteiro (Integer)
iex> 10
10

# Real (Float)
iex> 10.1
10.1

# Map
iex> %{id: 123, nome: "Foo"}
%{id: 123, nome: "Foo"}

iex> %{"id" => 123, "nome" => "Foo"}
%{"id" => 123, "nome" => "Foo"}

# Vetor/Lista (List)
iex> [:a, "b", 3]
[:a, "b", 3]

iex> [%{test: 1}, %{test: 2}, %{test: 3}]
[%{test: 1}, %{test: 2}, %{test: 3}]

# Tupla (Tuple)
iex> {:ok, []}
{:ok, []}

iex> {:a, "b", :c, 4}
{:a, "b", :c, 4}

# Binary
iex> <<1, 2, 3>>
<<1, 2, 3>>

# Char list
iex> 'aleDsz'
'aleDsz'

# Estrutura (Struct)
iex> defmodule User do
...>   defstruct [:id, nome]
...> end
iex> %User{}
%User{
  id: nil,
  nome: nil
}
```

### Átomos

Átomos por si só é uma constante que o valor é ele mesmo. Seu uso é bem comum quando utilizado em `pattern matching` (explicaremos isso mais a fundo na seção **Avançada**).

Usando isso como base, outro uso de átomos seria para a definição das chaves de um map (este que é definido por chave-valor).

### String

Como definido acima, as strings são binários, ou seja, exatamente como o C define uma string (um vetor de caracteres). Você pode tratar uma string como `binary` que, por sua vez, o `binary` não pode ser tratado como string por ter um tipo diferente.

### Map

Em POO, você cria uma entidade e instancia a mesma como um objeto para utilizar em seu sistema. Em Elixir, o qual não existe classes e objetos, você pode trabalhar com Maps que, resumidamente, é uma estrutura de chave-valor sem uma definição de tipo para o mesmo.

Em um Map, você pode definir as chaves como `string` ou `átomo`. _Structs_, por padrão, trabalham com chaves do tipo `átomo` e JSON convertido para Map trabalha com chaves do tipo `string`.

### Tupla

Resumidamente, uma tupla é uma lista com tamanho pré=definido, tendo como uso padrão, para retorno de funções e padronização do mesmo.

```elixir
# Uma lista com tamanho dinâmico
iex> [1, 2, 3]
[1, 2, 3]

iex> [1, 2, 3] ++ [4]
[1, 2, 3, 4]

# Uma lista com tamanho "pré=definido"
iex> {1, 2, 3}
{1, 2, 3}

# Calma, vamos explicar como funciona esse tal de pipe (|>)
iex> {1, 2, 3} |> Tuple.append(4)
{1, 2, 3, 4}
```

### Binary

Binário, não necessariamente trabalha com binário, pois este pode ser também:

 - uma representação de uma `string`;
 - uma representação de um conjunto de números que pode representar um caracter Unicode;
 - uma representação de um conjunto de números que pode representar um binário (neste caso, pode ser um executável, uma imagem, etc.).

### Char list

TODO: Criar uma explicação fodástica

### Struct

Uma Struct é um Map o qual define-se um tipo ao Map como um todo. Ou seja, quando queremos validar se um Map é, de fato, um dado que estamos esperando em uma estrutura pré-definida, a `Struct` é o que garante que aquele Map sempre terá tal chave em sua estrutura, mas não necessariamente com valor.

Em versões mais recentes do Elixir (1.9+), é possível você validar se um Map é apenas um Map ou se ele também é uma Struct ou não.

Em versões mais antigas (1.8-), isso é garantido através da chave `:__struct__` dentro do Map.