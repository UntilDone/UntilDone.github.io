+++
title = "Printf no bash"
date = 2021-04-14
updated = 2021-04-16
description = "Demonstração do commando printf"
draft = false

[taxonomies]
categories = ["Tutorial"]
tags = ["bash", "printf"]

[extra]
image = "https://upload.wikimedia.org/wikibooks/zh/0/06/Firefox.svg"
author = "Rômulo"


+++


# Introdução
```bash
printf format [argument]...
```

O comando printf do bash opera de forma parecida com a função printf em C/C++. Ele recebe como primeiro parametro _format_, uma string entre aspas duplas "como essa aqui" e pode receber alguns argumentos para auxiliar na formatação, como sequências de escape e referências para variáveis. 

# Sequência de escape
|Escape|Uso|
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
A forma mais direta de se usar o "print formated" é chamando o comando seguido de uma string entre aspas duplas. Assim ele vai imprimir na tela exatamente o que for pedido. Também é possível colocar uma string dentro de outra com ajuda do caractere de conversão para strings __%s__, tente aí no seu terminal e veja o que acontece.  
```bash
$ printf "O rato roeu a roupa do %s" "rei de roma."
```

<img src=/images/printf-output1.png title="Em nenhum momento pedimos ao printf que imprimisse uma nova linha"></img>

A frase saiu sem quebra de linha (nova linha). Pode não parecer agora, mas isso nos dá mais controle sobre o comportamento desse comando. Podemos consertar isso com uma sequencia de escape para nova linha.

<img src=/images/printf-output2.png title="uma string com uma quebra de linha no último caractere"></img>

# Números inteiros
Você pode colocar um espaço entre __%__ e __d__ em __%d__ para imprimir os números inteiros positivos com um espaço na frente. Isso ajuda na criação de uma coluna com a formatação mais homogênea, observe o exemplo feito das duas maneiras.  
```bash
$ printf "% d\n%d\n% d\n" 10 -10 10
```

<img src="/images/printf-output8.png" title=""></img>

# Números decimais
Quando se trata de números devemos especificar a quantidade de casas decimais, caso contrário recebe por padrão o valor seis. O zero à esquerda pode ser omitido sem problema.
```bash
$ printf "Preço - R$%.2f\nLitro - %.3f ml\nTemperatura - %.1f ºC\nPadrão - %f\n" 5.55 5.55 .55 0.55
```
<img src=/images/printf-output7.png></img>

# Caracteres Bandeira
O caractere __%__ é seguido por zero ou mais das seguintes flags.  

|Flag|Descrição|
|:---:|:---|
|__#__ |O valor será convertido para uma "forma alternativa". Para conversões __o__ o primeiro caractere da string de saída do comando |
|__0__ |O valor será precedido por um zero|
|__-__ |O valor convertido será alinhado à esquerda do campo delimitado (o padrão é alinhado à direita)|
|__' '__ |(um espaço) um espaço em branco deve ser deixado antes de um número positivo (ou uma string vazia)|
|__+__ |Um sinal (__+__ ou __-__) deve ser sempre colocado antes de um número produzido por conversão de sinais. Por padrão um sinal é usado apenas para números negativos. Um __+__ sobrescreve um espaço se ambos forem usados.|

Tenha em mente que o printf tenta converter para string para todos os argumentos.  
```bash
$ printf "Olá, %s! \n" Rômulo Pinheiro Costa

```
<img src=/images/printf-output3.png title="%s é substituído pelo próximo parametro do tipo string"></img>

## Tipos de variáveis
```bash
$ printf "Resolva a equação:  %d + %f = X\n" $inteiro $decimal	
```
<img src=/images/printf-output4.png></img>  
  
Talvez você tenha que adicionar esta variavel de ambiente no seu bash para que sejam impressos corretamente os pontos flutuantes L_C_NUMERIC=en_US.UTF-8_  

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

