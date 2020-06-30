# 3.4 - Tudo é uma Expressão

Quando dizemos que no Elixir tudo é considerado uma expressão é por conta que Elixir sempre retorna um resultado. Isso acontece por que dentro dele tudo é considerado uma expressão e toda expressão deve retornar um valor, ou seja não há declarações sem retorno de algum valor. Por exemplo os códigos abaixo que foram feitos como exemplo para explicar o Paradigma da linguagem, irei replicar os mesmos acrescentado alguns comentarios para que vocês entenda.

```elixir
# Basicamente estamos declarando uma variavel aqui, e como disse não temos declarações sem retorno de valor. Então ele vai simplesmente imprimir para a gente o valor da variavel, comparando com linguagens imperativas o ato de declarar a variavel não ia trazer para gente nenhum retorno a não ser se a gente fizesse de maneira implícita. O mesmo comportamento acontece nos códigos abaixo deste.
iex> idade = 20
20

# Função anônima para alterar a idade
iex> funcao = (fn -> idade = 30 end)
#Function<20.128620087/0 in :erl_eval.expr/5>

# Execução da função
iex> funcao.()
30

# Exibição da "variável"
IO.inspect idade
20
```

Então sabendo disso o nosso programa em si fica melhor e mais légivel, natural por que cada instrução sempre vai retornar alguma coisa por si mesma, isso acaba deixando o fluxo da execução do nosso programa bem mais evidente.

# Observações

- Sabendo que no Elixir tudo é tratado como uma expressão e toda expressão retorna algo então a gente não precisa declarar um return, ele sempre vai retornar a ultima expressão.