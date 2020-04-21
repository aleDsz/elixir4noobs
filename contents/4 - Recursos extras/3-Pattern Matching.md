# 4.3 Pattern Matching

Esse aqui, esse aqui é o motivo que você irá amar o Elixir, pois *pattern matching* é a base de tudo que é maravilhoso nesse mundo de alquimistas.

Em outras linguagens, quando você precisa criar uma função com o mesmo nome, você acaba precisando aumentar os parâmetros ou até utilizar vários *if*'s para conseguir ter processamentos diferentes para dados diferentes:

```php
class Foo {
  public function getUser (Array $params) {
    if (!isset($params["type"])) {
      return null;
    }

    if ($params["type"] === "admin") {
      return getAdmin($params);
    }

    if ($params["type"] === "client") {
      return getClient($params);
    }

    $user = getFromDatabase("user", $params["id"]);
    return $user;
  }
}
```

No exemplo acima, fora necessário validar o campo `type` dentro do array de parâmetros para executar funções diferentes para obter um usuário pelo seu ID.

Se gerarmos um exemplo parecido em Elixir, ele ficaria muito mais simples:

```elixir
defmodule Foo do
  def get_user(%{"id" => user_id, "type" => "admin"}) do
    case User.get(user_id) do
      {:ok, user} ->
        {:ok, user}

      {:error, reason} ->
        {:error, reason}
    end
  end
  def get_user(%{"id" => user_id, "type" => "client"}) do
    case User.get(user_id) do
      {:ok, user} ->
        {:ok, user}

      {:error, reason} ->
        {:error, reason}
    end
  end
  def get_user(%{"id" => user_id, "type" => "user"}) do
    case User.get(user_id) do
      {:ok, user} ->
        {:ok, user}

      {:error, reason} ->
        {:error, reason}
    end
  end
  def get_user(_params), do: nil
end
```

Você consegue realizar validações, obter dados diretamente dos parâmetros de uma função utilizando as técnicas ninjas de *pattern matching*.

Para melhorar seu entendimento, colocarei mais exemplos abaixo:

- Utilizando validação de tamanho de string para realizar o *pattern matching*:

```elixir
defmodule Foo do
  def validate_document(<<document::binary-size(14)>>),
    do: :valid_cnpj

  def validate_document(<<document::binary-size(11)>>),
    do: :valid_cpf

  def validate_document(_document),
    do: :invalid
end
```

- Utilizando guards para validar os tipos dos dados com o *pattern matching*:

```elixir
defmodule Bar do
  def get_user(user_id) when is_integer(user_id),
    do: user_id |> Users.get()

  def get_user(user_id) when is_binary(user_id),
    do: user_id |> String.to_integer() |> Users.get()

  def get_user(%{"id" => user_id}) when is_integer(user_id),
    do: user_id |> Users.get()

  def get_user(%{"id" => user_id}) when is_binary(user_id),
    do: user_id |> String.to_integer() |> Users.get()
end
```

- Utilizando átomos e guards para realizar o *pattern matching*:

```elixir
defmodule Elixir4Noobs do
  def calcular(:sum, number1, number2) when is_integer(number1) and is_integer(number2),
    do: number1 + number2

  def calcular(:subtract, number1, number2) when is_integer(number1) and is_integer(number2),
    do: number1 - number2

  def calcular(:division, number1, number2) when is_integer(number1) and is_integer(number2),
    do: number1 / number2

  def calcular(:multiply, number1, number2) when is_integer(number1) and is_integer(number2),
    do: number1 + number2
end
```