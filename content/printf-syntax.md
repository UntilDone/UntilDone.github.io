+++
title = "Printf no bash"
date = 2021-04-14
updated = 2021-04-16
description = "Demonstra a sintaxe do commando printf"
draft = false

[taxonomies]
categories = ["Tutorial"]
tags = ["bash", "printf"]

[extra]
image = "https://upload.wikimedia.org/wikibooks/zh/0/06/Firefox.svg"
author = "Rômulo Pinheiro"


+++


# Introdução
```bash
$ printf format [argument]...
```

O comando printf do bash opera de forma parecida com a função printf em C/C++. Ele recebe como primeiro parametro _format_, uma string entre aspas duplas "como essa aqui" e pode receber alguns argumentos para auxiliar na formatação. O comando também aceita sequências de escape. você pode encontrar uma lista de exemplos logo abaixo da tabela com as sequências de escapes.  

# Sequência de escape
|caracter|uso|
|:---:|:---|
|\\" | aspas duplas|
|\\\ | contrabarra|
|\a | alerta|
|\b | backspace|
|\c | não produz output a mais|
|\e | esc|
|\f | campo de formulário|
|\n | nova linha|
|\r | enter|
|\t | tabulação horizontal|
|\v | tabulação vertical|
|\NNN | byte com valor octal (1 a 3 digitos)
|\xHH | byte com valor hexadecimal HH (1 a 2 digitos)
|\uHHHH | caractere unicode (ISO/IEC 10646) hexadecimal HHHH (4 digitos)
|\UHHHHHHHH | caractere unicode com valor hexdecimal (8 digitos)
|\%\% | um único símbolo de porcentagem|
|\%b | argumento string que contenha sequencias de escape|
|\%q | argumento é imprimido em formato que pode ser reusado como input do shell com a sintaxe $''

# Strings
```bash 
$ printf "Resolva a equação:  2 + 2.5 = X"  
```
<img src=/images/printf-output1.png title="Em nenhum momento pedimos ao printf que imprimisse uma nova linha"></img>

```bash
$ printf "Resolva a equação:  2 + 2.5 = X\n"

```
<img src=/images/printf-output2.png title="uma string com uma quebra de linha no último caractere"></img>

# Números inteiros

# Números decimais
```bash
$ printf "Resolva a equação:  R$%.2f + R$%.2f = R$ X\n" $decimal1 $decimal2
```
<img src=/images/printf-output7.png></img>

# Formatação
```bash
$ printf "Resolva a %s:  2 + 2.5 = X\n" "equação"

```
<img src=/images/printf-output3.png title="%s é substituído pelo próximo parametro do tipo string"></img>

## Tipos de variáveis
```bash
$ printf "Resolva a equação:  %d + %f = X\n" $inteiro $decimal	
```
<img src=/images/printf-output4.png></img>

>Talvez você tenha que adicionar esta variavel de ambiente no seu bash para que sejam impressos corretamente os pontos flutuantes L_C_NUMERIC=en_US.UTF-8_

## Alinhamento à direita
```bash
$ printf "Resolva a equação: |%15s + %15s = %s|\n" "dezesseis" "um" "dezessete"

```
<img src=/images/printf-output5.png></img>
	
## Alinhamento à esquerda
```bash
$ printf "Resolva a equação: |%-15s + %-15s = %s|\n" "dezesseis" "um" "dezessete"
```
<img src=/images/printf-output6.png></img>

