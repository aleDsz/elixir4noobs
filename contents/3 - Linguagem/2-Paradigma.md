## 3.2 - Paradigma

De maneira simples, o paradigma funcional é uma sequência de funções e/ou passos os quais meu código executará para resolver um problema.

Diferentemente da [Programação Orientado a Objetos](https://pt.wikipedia.org/wiki/Orienta%C3%A7%C3%A3o_a_objetos) (POO), ele não trabalha em cima de entidades que possuem características e comportamentos, ou seja, você apenas orienta o seu sistema em quais passos, utilizando funções, o dado de entrada do seu sistema irá passar até o ponto em que ele se tornar o dado de saída.

## Imutabilidade

Na programação funcional uma variável não é de fato uma viarável pois a imutabilidade proíbe que os dados variem. Mas não se preocupe, não leve isso para o literal, pois explicarei direitinho como isso funciona no decorrer do curso.

Para explicar melhor, irei citar um artigo do [Medium](https://medium.com/trainingcenter/programa%C3%A7%C3%A3o-funcional-para-iniciantes-9e2beddb5b43) que exemplifica bem essa ideia:

    A imutabilidade faz sentido dentro da programação funcional pelo seu viés matemático. Nela, um número sempre será aquele valor, independente de onde esteja ou como está sendo usado. É importante também entender que nas expressões matemáticas, para um mesmo valor passado a uma variável, teremos o mesmo retorno da função. Ele nunca muda. Se você tem uma expressão como f(x) = x + 2, você pode passar o número 3 quantas vezes quiser, esta função sempre retornará 5. Um último ponto é que o número 3 passado para x, não irá mudar seu valor, ou seja, ele permanece inalterado após o seu uso na função.

Entendendo o que fora citado acima, podemos dizer que tudo que está fora do mesmo contexto, não altera os dados de outros contextos.

Para entender melhor, podemos seguir com este código:

```elixir
# Definição da "variável"
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

No código acima, percebemos que a variável `idade` não teve seu valor original alterado pela função anônima `funcao`.