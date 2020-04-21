# 4.2º Testes

Testa, mas testa mesmo, isso que você precisa, dos amados Testes. Todo desenvolvedor que quer manter seu projeto funcional conforme o passar do tempo, **precisa** fazer testes, sejam eles unitários ou *end-to-end*.

O mais simples de se explicar é usando o teste unitário, pois esse não precisa configurar um case de test para API (Phoenix, Plug, etc.).

```elixir
# my-app/test/algum_test.exs

defmodule MyApp.AlgumTest do
  use ExUnit.Case, async: false

  test "uno teste mui bonito" do
    assert true
  end

  test "uno teste mui refutada" do
    refute false
  end
end
```

Ao executar o `mix test` seu teste será executado e você poderá ver quantos deram sucesso, mas se quiser que ele seja verboso, utilize o comando `mix test --trace`.

Caso você queira fazer tests **end-to-end**, você precisa ver a documentação da biblioteca que você for usar para gerar uma API:

- [Phoenix](https://hexdocs.pm/phoenix)
- [Maru](https://hexdocs.pm/maru)
- [Plug](https://hexdocs.pm/plug)