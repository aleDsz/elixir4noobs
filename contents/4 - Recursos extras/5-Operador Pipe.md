# 4.5 Operador Pipe

O operador pipe `|>` passa o resultado de uma expressão como o primeiro parâmetro de outra expressão. Com ele podemos escrever códigos simples e muito mais elegantes. Exemplos abaixo:

Imagine que eu tenha a seguinte string:

```elixir
iex(1)> string = " eLiXir4NoObS \n "
" eLiXir4NoObS \n "
```
Entretanto, eu gostaria de gerar uma string sem os `espaços`, sem esse `\n` e sem essas letras `maiúsculas`. Bom, uma opção que eu poderia fazer seria chamar a função `String.trim/1` passando a minha própria `string`.

```elixir
iex(2)> String.trim(string)
"eLiXir4NoObS"
```
Dito isso, podemos ver que ele removeu os espaços e também o `\n`. Porém, estamos em uma `linguagem imutável`. Logo, a gente precisa atribuir a nossa `string` novamente.

```elixir
iex(3)> string = String.trim(string)
"eLiXir4NoObS"
iex(4)> string
"eLiXir4NoObS"
```

Agora sim estamos com a nossa ``string`` modificada. Para deixarmos com letras minúsculas, teriamos que novamente atribuir a ``string`` recebendo a função ``String.downcase/1``.

```elixir
iex(5)> string = String.downcase(string)
"elixir4noobs"
iex(6)> string
"elixir4noobs"
```
Pronto! Aí está a nossa ``string`` sem os ``espaço``, sem ``\n`` e sem as ``letras maiúsculas``. Ou seja, primeiro a gente precisou atribuir a nossa ``váriavel``, depois tivemos que fazer o ``trim`` e por fim o ``downcase``, isso tudo atribuindo. São nesses cenários que a gente pode usar o ``pipe operator``.

## Utilizando o Pipe Operator

Veja como é bem mais fácil produzir código mais legíveis e elegante, um operador muito legal em ``Elixir`` para deixar nosso código mais elegante e fácil de entender!

```elixir
iex(7)> " eLiXir4NoObS \n " |> String.trim() |> String.downcase()
"elixir4noobs"
```

O que o ``pipe operator`` faz? Bom, ele nada mais faz do que pegar o resultado de qualquer operação antes dele e passa para a função seguinte como primeiro argumento. Ou seja, estamos pegando ``" eLiXir4NoObS \n "`` passando para a função ``String.trim()`` e com o resultado da função ``trim()`` estamos passando para ``String.downcase()`` sempre como o primeiro argumento.

---

Mais informações, consulte a [documentação Elixir School](https://elixirschool.com/pt/lessons/basics/pipe_operator)