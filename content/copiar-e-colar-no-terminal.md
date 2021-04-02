+++
title = "Copiar e colar no terminal"
description = "Explica como copiar e colar dentro e fora do temrminal."
date = 2021-03-23
thumbnail = "https://upload.wikimedia.org/wikipedia/commons/5/55/Tux_Enhanced.svg"
tags = ["xclip", "alias", "bash"]

[extra]
author = "Rômulo Pinheiro"
+++

`CTRL`+`C` e `CTRL`+`V` são atalhos muito úteis no dia-a-dia. Acontece q se você é usuário da linha de comando, já deve ter percebido que o atalho `CTRL`+`C` está associado com a interrupção do processo em andamento.


### **Copiar e colar com alias**.

Mas e se precisarmos copiar um documento inteiro, ou colar o conteúdo de algum arquivo diretamente em outro? Usar os atalhos do gnome seria cansativo e repetitivo, especialmente se precisarmos copiar e colar com certa frequência. Nessa horas um alias pode ajudar. E para criar um no bash é muito simples, basta adicionar uma linha no arquivo _.bashrc_ que fica localizado na pasta raiz do usuário com a seguinte sintaxe:  

`alias nome_do_alias="comando-a-ser-executado"`  

A declaração de um alias começa com a palavra chave reservada _alias_ seguida do nome que você escolher para esse alias, o sinal de igual `=` e por fim o comando desejado escrito dentro de aspas. Cada alias precisa ser declarado em uma nova linha.

>**Atalho do terminal Gnome**
>
>Para copiar o texto selecionado dentro do terminal você também pode utilizar o atalho `CTRL`+`SHIFT`+`C` e colar com `CTRL`+`SHIFT`+`V`.

### **Copiar e colar com xclip**

A ferramenta _xclip_ é fácil de usar se encaixa bem pra essa tarefa. Vamos criar logo um alias para copiar e outro para colar, que mais abaixo deixo uma explicação de como eles funcionam.

**Copiar**  
`alias xcopy="xclip -selection clipboard"`  

**Colar**  
`alias xpaste="xclip -selection clipboard -o"`  

_xclip_ é o comando principal que vai copiar ou colar algum conteúdo pra gente. A opção _-selection_ vai dizer pra ele **onde** vai realizada essa tarefa, que pode trabalhar com três opções: _primary_, _secondary_, e _clipboard_. O parametro clipboard diz ao _xclip_ que queremos copiar para a **área de transferência** aquilo que for selecionado. E por fim a opção `-o` que quando adicionada diz  a ele que o que estiver sido selecionado deve ser redirecionado para a **saída** do programa.

Agora experimente copiar com:  

`$ xcopy nome_do_arquivo`  

e colar com:  
`$ xpaste`  

Eles também aceitam redirecionamento!  

`$ man xclip | xcopy`  

`$ xpaste > manual.txt`  

