## 2.1 - Como começar?

Se você chegou nesse passo, acredito que esteja pensando em qual IDE ou qual editor de texto você precisa instalar para começar a desenvolver.

Bom, você não precisa se preocupar tanto com isso, pois você pode usar até um bloco de notas para tal 😅

Brincadeiras a parte, você escolher estes editores:

 - [Sublime Text 3](https://www.sublimetext.com/3)
 - [Visual Studio Code](https://code.visualstudio.com/download)
 - [Atom](https://atom.io/)
 - [Vim](https://www.vim.org/download.php)

Para que seu desenvolvimento seja mais intuitivo, você pode instalar esta lista de extensões para cada Editor de texto acima:

## Extensões

### Sublime text

Para instalar as extensões para o Sublime Text, você precisa destas extensões:

 - Elixir
 - ElixirSublime
 - ElixirSyntax

Para isso, você precisa instalar o [Controle de Pacotes do Sublime](https://packagecontrol.io/installation#st3) e depois executar os comandos em seu Sublime Text:

1. `Control + Shift + P` (Windows/Linux) ou `Command + Shift + P` (macOS)
2. Digitar `Package Control: Install Package` e pressionar `Enter`.
3. Digitar o nome dos pacotes, um por um, e pressionar `Enter`.

### Visual Studio Code

Para instalar as extensões para o Visual Studio Code, você precisa destas extensões:

 - ElixirLS: Elixir support and debugger
 - vscode-elixir
 - vscode-elixir-syntax

Para isso, você precisa executar os comandos em seu Visual Studio Code:

1. `Control + Shift + X` (Windows/Linux) ou `Command + Shift + X` (macOS)
2. Digitar o nome das extensões, um por um, e clicar em `Install`.

### Atom

Para instalar as extensões para o Atom, você precisa destas extensões:

 - atom-ide-ui
 - ide-elixir

Para isso, você precisa executar os comandos em seu Atom:

```sh
apm install atom-ide-ui
apm install ide-elixir
```

### Vim

Para instalar as extensões para o Vim, você precisa destas extensões:

 - vim-elixir
 - coc.nvim
 - coc-elixir

Se você utiliza Vim, você sabe que é necessário instalar tudo pelo arquivo `.vimrc`.

Porém, para instalar o `coc-elixir`, você precisa rodar este comando no Vim:

```sh
:CocInstall coc-elixir
```