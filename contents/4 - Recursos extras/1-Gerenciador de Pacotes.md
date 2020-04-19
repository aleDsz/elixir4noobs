# 4.1 Gerenciador de Pacotes

Assim como em outras linguagem, como o [amado] Javascript, o Elixir também usa um e este é chamado de `mix`. Com ele, criamos projetos, executamos tasks, testes e faz café também (brincadeira, mas poderia não ser 😞)).

```sh
# Criar novo pacote
$ mix new lind-ex

# Criar novo app
$ mix new appzao --sup

# Testes
$ mix test

# Rodar uma task customizada
$ mix task aquela.fcking.task

# Instalar dependências
$ mix deps.get

# Compilar todas as dependências
$ mix deps.compile

# Compilar uma dependência
$ mix deps.compile lind-ex

# Atualizar uma dependência
$ mix deps.update lind-ex

# Compilar projeto
$ mix compile

# Rodar arquivo utilizando dependências do projeto
$ mix run lib/aquele/arquivo/foda.ex

# Rodar projeto sem encerrar
$ mix run --no-halt

# Rodar projeto usando Phoenix
$ mix phx.server
```

**Curiosidade:** É comum você definir em alguma parte do nome do seu projeto, algo relacionado com **ex** pois este define que o seu projeto é feito em Elixir.


## Terminal Interativo

Assim como o Python, é possível executar código em um terminal interativo, mas no Elixir é possível fazer de algumas formas:

1) Sem as dependências:

```sh
iex

# Executado:
Interactive Elixir (1.8.2) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)>
```

2) Sem as dependências utilizando um `node` nomeado:

```sh
iex --sname nome@localhost

# Executado:
Interactive Elixir (1.8.2) - press Ctrl+C to exit (type h() ENTER for help)
iex(nome@localhost)1>
```

3) Com as dependências:

```sh
iex -S mix

# Executado:
Interactive Elixir (1.8.2) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)>
```

4) Com as dependências utilizando um `node` nomeado:

```sh
iex --sname nome@localhost -S mix

# Executado:
Interactive Elixir (1.8.2) - press Ctrl+C to exit (type h() ENTER for help)
iex(nome@localhost)1>
```

**Curiosidade:** Você pode executar o comando `iex -S mix phx.server` caso queira rodar um projeto Phoenix com API ativa dentro do terminal interativo, para testar algumas funções diretamente e conseguir realizar requests pra sua API.