---
layout: post
title: Como copiar e colar no terminal
date: 2021-03-23
categories: Bash, copiar, colar, xclip, linha de comando
published: true
---
![webp](https://raw.githubusercontent.com/PinheiroCosta/PinheiroCosta.github.io/master/_images/terminal.webp)

```CTRL+C``` e ```CTRL+V``` são atalhos muito úteis no dia-a-dia. Acontece que se você é usuário da linha de comando, já deve ter percebido que o atalho ```CTRL+C``` está associado com a interrupção do processo em andamento.

>**Atalho do terminal Gnome**
>
>Para copiar o texto selecionado dentro do terminal você pode utilizar o atalho ```CTRL+SHIFT+C``` e colar com ``` CTRL+SHIFT+V```.


### **Copiar e colar com alias**.

Mas e se precisarmos copiar um documento inteiro, ou colar o conteúdo de algum arquivo diretamente em outro? Usar os atalhos do gnome seria cansativo e repetitivo, especialmente se precisarmos copiar e colar com certa frequência. Nessas horas um alias pode ajudar. E para criar um no bash é muito simples, basta adicionar uma linha no arquivo _.bashrc_ que fica localizado na pasta raiz do usuário com a seguinte sintaxe:
```ruby
alias nome_do_alias="comando-a-ser-executado"
```
A declaração de um alias começa com a palavra chave reservada _alias_ seguida do nome que você escolher para esse alias, o sinal de igual ```=``` e por fim o comando desejado escrito dentro de aspas. Cada alias precisa ser declarado em uma nova linha.

### **Copiar e colar com xclip**

A ferramenta _xclip_ é fácil de usar se encaixa bem pra essa tarefa. Vamos criar logo um alias para copiar e outro para colar, que mais abaixo deixo uma explicação de como eles funcionam.

**Copiar**
```ruby
alias xcopy="xclip -selection clipboard"
```

**Colar**
```ruby
alias xpaste="xclip -selection clipboard -o"
```

_xclip_ é o comando principal que vai copiar ou colar algum conteúdo pra gente. A opção _-selection_ vai dizer pra ele **onde** vai realizada essa tarefa, que pode trabalhar com três opções: _primary_, _secondary_, e _clipboard_. O parametro clipboard diz ao _xclip_ que queremos copiar para a **área de transferência** aquilo que for selecionado. E por fim a opção ```-o``` que quando adicionada diz  a ele que o que estiver sido selecionado deve ser redirecionado para a **saída** do programa.

Agora experimente copiar com:

```ruby
xcopy nome_do_arquivo
```

e colar com:
```ruby
xpaste
```

Eles também aceitam redirecionamento!

```ruby
man xclip | xcopy
```

```ruby
xpaste > manual.txt
```


