# 1.2 - Pré-requisitos

## Conhecimentos Necessários

Para que você possa compreender tranquilamente neste curso, é necessário que você tenha conhecimentos básicos em qualquer outra linguagem, por exemplo:

  * PHP
  * Javascript
  * Ruby (preferencialmente)
  * Python
  * C#
  * Java

Qualquer uma destas linguagens acima, já é o suficiente. Mas claro, se você souber outra linguagem que não esteja listada, também será bem útil para prosseguirmos.

## Instalação

Para começarmos, precisamos instalar o **Elixir** e **Erlang** em seu ambiente. Para isso, existem algumas formas de se instalar ambas as linguagens.

### Erlang

#### Windows

No Windows conseguimos instalar via [web](http://www.erlang.org/download.html) ou via [chocolatey](https://chocolatey.org/).

Para instalar via Chocolatey, você pode executar via PowerShell ou pelo Prompt de Comando.

**Lembrando que ambos precisam executar como administrador**

```batch
# Novas versões do Chocolatey
cinst erlang

# Versões antigas do Chocolatey
choco install erlang
```

#### macOS

No Mac conseguimos instalar via Homebrew ou Macports.

Para instalar via Homebrew, você executará em ser terminal:

```sh
brew install erlang
```

Para instalar via Macports, você executará em ser terminal:

```sh
sudo port install erlang
```

#### Unix

 * Ubuntu/Linuxmint:

   Para instalar no Ubuntu ou Linuxmint, é necessário adicionar o repositório do Erlang na sua lista de pacotes do Aptitude.

   Para isso, é necessário executar alguns comandos no seu terminal:

   ```sh
   # Atualizar lista de pacotes
   sudo apt-get update
   sudo apt-get -y upgrade

   # Adicionar lista de pacotes ao Aptitude
   wget https://packages.erlang-solutions.com/erlang-solutions_2.0_all.deb
   sudo dpkg -i erlang-solutions_2.0_all.deb

   # Instalar o Erlang
   sudo apt-get update
   sudo apt-get install esl-erlang
   ```

 * Arch Linux:

   Para instalar no Arch Linux é necessário executar apenas um comando no seu terminal:

   ```sh
   pacman -S erlang
   ```

 * openSUSE:

   Para instalar no openSUSE é necessário adicionar o repositório do Erlang na sua lista de pacotes.

   Para isso, é necessário executar alguns comandos no seu terminal:

   ```sh
   zypper ar -f obs://devel:languages:erlang:Factory Erlang-Factor
   zypper install erlang
   ```

### Elixir

#### Windows

No Windows conseguimos instalar via [web](https://repo.hex.pm/elixir-websetup.exe) ou via [chocolatey](https://chocolatey.org/).

Para instalar via Chocolatey, você pode executar via PowerShell ou pelo Prompt de Comando.

**Lembrando que ambos precisam executar como administrador**

```batch
# Novas versões do Chocolatey
cinst elixir

# Versões antigas do Chocolatey
choco install elixir
```

#### macOS

No Mac conseguimos instalar via Homebrew ou Macports.

Para instalar via Homebrew, você executará em ser terminal:

```sh
brew install elixir
```

Para instalar via Macports, você executará em ser terminal:

```sh
sudo port install elixir
```

#### Unix

 * Ubuntu/Linuxmint:

   Para instalar no Ubuntu ou Linuxmint é necessário executar alguns comandos no seu terminal:

   ```sh
   # Instalar o Elixir
   sudo apt-get update
   sudo apt-get install elixir
   ```

 * Arch Linux:

   Para instalar no Arch Linux é necessário executar apenas um comando no seu terminal:

   ```sh
   pacman -S elixir
   ```

 * openSUSE:

   Para instalar no openSUSE é necessário executar alguns comandos no seu terminal:

   ```sh
   zypper ar -f obs://devel:languages:erlang/ Elixir-Factory
   zypper refresh
   zypper install elixir
   ```


**OBS.:** Para que tudo funcione corretamente, é estritamente necessário que Elixir e Erlang estejam instalados em seu computador.

Para testar a instalação de ambos, você pode executar este comando em seu terminal:

```
→ C:\Users\aleDsz› elixir --version
Erlang/OTP 21 [erts-10.2] [64-bit] [smp:12:12] [ds:12:12:10] [async-threads:1]

Elixir 1.8.2 (compiled with Erlang/OTP 20)
```

Para continuar, é válido frisar que o curso foi feito em cima do Elixir na versão **1.8.2**