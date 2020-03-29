# 3.1 - Sobre a linguagem

Elixir é uma linguagem de programação funcional, concorrente, de propósito geral que executa na máquina virtual Erlang (BEAM). Elixir compila em cima de Erlang para fornecer aplicações distribuídas, em tempo real suave, tolerante a falhas, non-stop, mas também a estende para suportar metaprogramação com macros e polimorfismo via protocolos.

José Valim é o criador da linguagem de programação Elixir, um projecto de R&D da Plataformatec, uma subsidiária do Nubank. Seus objetivos foram permitir uma maior extensibilidade e produtividade no Erlang VM, mantendo a compatibilidade com ferramentas e ecossistema de Erlang.

## Extensão

No Elixir, os arquivos que precisam serem compilados no projeto necessariamente são salvos como `.ex`.

Quando você cria um arquivo que não será compilado, você irá salvá-lo como `.exs`, como é o caso dos testes unitários.

Existem outras extensões como `.eex`, que este é interpretado pelo EEx, que é uma aplicação do Elixir para leitura e interpretação de código Elixir para gerar uma valor final.

Um exemplo disso é a renderização de HTML, que pode conter código Elixir no meio deste, mas só é interpretado quando renderizado pelo [EEx](https://elixirschool.com/pt/lessons/specifics/eex/) (Elixir embutido).