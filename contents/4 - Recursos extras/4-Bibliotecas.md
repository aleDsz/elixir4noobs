# 4.4 Bibliotecas

## Phoenix

Uma das bibliotecas mais importantes para começar a estudar para a construção de API's, utilizando o *real-MVC*, como é considerado no mercado atual. Ele consiste em criar uma interface mais amigável aos desenvolvedores na hora de construir uma API estruturada e com os paradigmas funcionais.

Para instalar, você precisa instalar o hex local para instalar como dependência global (igual o npm e yarn)

```sh
$ mix local.hex --force
$ mix archive.install hex phx_new <version> # 1.4.16
```

Após a instalação, você pode instalar, ao invés de usar o `mix new`, você utilizará um comando específico para criar projetos Phoenix:

```sh
$ mix phx.new hello_world
```


Mais informações, consulte a [documentação do Phoenix](https://hexdocs.pm/phoenix/installation.html)

## Ecto

Todos amamos o uso de ORM para realizarmos consultas no banco de dados, e para isso criou-se a dependência `Ecto`, no qual consiste em criar uma interface com *schemas* para coordenar as tabelas, gerar validações e realizar consultas sem a necessidade de escrever SQL puro. E pasmem, tudo isso utilizando a sintaxe do Elixir:

```elixir
defmodule MyApp.Schemas.User do
  @moduledoc """
  Schema representation for `users` table
  """
  use Ecto.Schema
  import Ecto.Changeset

  @primary_key {:id, :binary_id, autogenerate: true}

  schema "users" do
    field :name, :string
    field :age, :integer
    field :status, :string, default: "inactive"

    timestamps()
  end

  @doc """
  Generate changeset for schema using JSON as parameters
  """
  def changeset(%__MODULE__{} = schema, attrs) do
    schema
    |> cast(attrs, [:name, :age, :status])
    |> validate_required([:name, :age, :status])
    |> validate_inclusion(:status, ~w(active inactive))
  end
end
```

Usando o exemplo acima, temos um schema da tabela `users` onde temos 3 campos (sem contar o campo `:id`, pois ele é gerado automaticamente).

Além disso, estamos:

1) Recebendo campos específicos utilizando a função `cast/2`;
2) Validando se os campos "castados" não são `nil` ou `empty_string`;
3) Validando se no campos `:status`, os dados inseridos fazem parte do enum de `["active", "inactive"]`.

**Curiosidade:** Esse schema utiliza `:binary_id` como ID, o qual é geralmente utilizado pelo Postgres.