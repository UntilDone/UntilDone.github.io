+++
title = "Printf no bash"
date = 2021-04-14
description = "Demonstra a sintaxe do commando printf"

[taxonomies]
categories = ["Tutorial"]
tags = ["bash", "printf"]

[extra]
image = "https://upload.wikimedia.org/wikibooks/zh/0/06/Firefox.svg"
author = "Rômulo Pinheiro"


+++


# Sinopse:
```bash
$ printf format [argument]...
```

O comando printf do bash opera de forma parecida com a função printf em C/C++. Ele recebe como primeiro parametro uma string entre aspas duplas "como essa aqui" podendo receber outras variaveis para serem incluídas na string com a ajuda de algumas diretrizes e sequências de escape. Segue abaixo uma lista de exemplos.  

# sequencia de escape
|caracter|uso|
|:---:|:---|
|\n| nova linha|
|\t| tabulação|
|\\| contrabarra|
|\%| símbolo de porcentagem|

# strings
```bash 
$ printf "Resolva a equação:  2 + 2.5 = X"  
```
<img src=/images/printf-output1.png></img>

```bash
$ printf "Resolva a equação:  2 + 2.5 = X\n"

```
![png2](/images/printf-output2.png)

## substituição
```bash
$ printf "Resolva a %s:  2 + 2.5 = X\n" "equação"

```
>Note a diretriz de string _%s_ que será substituída pela string informada
![png3]("images/printf-output3.png")

## tipos diferentes de variáveis
```bash
$ printf "Resolva a equação:  %d + %f = X\n" $inteiro $decimal	
```
![png4]("images/printf-output4.png")

>Talvez você tenha que adicionar esta variavel de ambiente no seu bash para que sejam impressos corretamente os pontos flutuantes L_C_NUMERIC=en_US.UTF-8_

## alinhamento à direita
```bash
$ printf "Resolva a equação: |%15s + %15s = %s|\n" "dezesseis" "um" "dezessete"

```
![png6]("images/printf-output6.png")
	
## alinhamento à esquerda
```bash
$ printf "Resolva a equação: |%-15s + %-15s = %s|\n" "dezesseis" "um" "dezessete"
```
 
# números inteiros

# números decimais
```bash
$ printf "Resolva a equação:  R$%.2f + R$%.2f = R$ X\n" $decimal1 $decimal2
```
![png5]("images/printf-output5.png")

