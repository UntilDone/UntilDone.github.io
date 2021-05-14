+++
title = "Printf no bash"
date = 2021-04-14
updated = 2021-04-16
description = "Como utilizar o commando printf na linha de comando"
draft = false

[taxonomies]
categories = ["Tutorial"]
tags = ["bash", "printf"]

[extra]
image = "https://upload.wikimedia.org/wikipedia/commons/thumb/4/4b/Bash_Logo_Colored.svg/512px-Bash_Logo_Colored.svg.png"
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
|__\\"__ | aspas duplas|
|__\ \\__ | contrabarra|
|__\a__ | alerta|
|__\b__ | backspace|
|__\c__ | não produz output a mais|
|__\e__ | esc|
|__\f__ | campo de formulário|
|__\n__ | nova linha|
|__\r__ | enter|
|__\t__ | tabulação horizontal|
|__\v__ | tabulação vertical|
|__\NNN__ | byte com valor octal (1 a 3 digitos)
|__\xHH__ | byte com valor hexadecimal HH (1 a 2 digitos)
|__\uHHHH__ | caractere unicode (ISO/IEC 10646) hexadecimal HHHH (4 digitos)
|__\UHHHHHHHH__ | caractere unicode com valor hexdecimal (8 digitos)
|__\%\%__ | um único símbolo de porcentagem|
|__\%b__ | argumento string que contenha sequencias de escape|
|__\%q__ | argumento é imprimido em formato que pode ser reusado como input do shell com a sintaxe $''

# Tipos de variáveis
Tenha em mente que o printf tenta converter para string para todos os argumentos.  
```bash
$ printf "Olá, %s! \n" Rômulo Pinheiro Costa

```
<img src=/images/printf-output3.png title="%s é substituído pelo próximo parametro do tipo string"></img>


## Strings
A forma mais direta de se usar o "print formated" é chamando o comando seguido de uma string entre aspas duplas. Assim ele vai imprimir na tela exatamente o que for pedido. Também é possível colocar uma string dentro de outra com ajuda do caractere de conversão para strings __%s__, tente aí no seu terminal e veja o que acontece.  
```bash
$ printf "O rato roeu a roupa do %s" "rei de roma."
```

<img src=/images/printf-output1.png title="Em nenhum momento pedimos ao printf que imprimisse uma nova linha"></img>

A frase saiu sem quebra de linha (nova linha). Pode não parecer agora, mas isso nos dá mais controle sobre o comportamento desse comando. Podemos consertar isso com uma sequencia de escape para nova linha.

<img src=/images/printf-output2.png title="uma string com uma quebra de linha no último caractere"></img>

## Números inteiros
Você pode colocar um espaço entre __%__ e __d__ em __%d__ para imprimir os números inteiros positivos com um espaço na frente. Isso ajuda na criação de uma coluna com a formatação mais homogênea, observe o exemplo feito das duas maneiras.  
```bash
$ printf "% d\n%d\n% d\n" 10 -10 10
```

<img src="/images/printf-output8.png" title=""></img>

## Números decimais
Quando se trata de números devemos especificar a quantidade de casas decimais, caso contrário recebe por padrão o valor seis. O zero à esquerda pode ser omitido sem problema.
```bash
$ printf "Preço - R$%.2f\nLitro - %.3f ml\nTemperatura - %.1f ºC\nPadrão - %f\n" 5.55 5.55 .55 0.55
```
<img src=/images/printf-output7.png></img>

Para operações matemáticas talvez você tenha que adicionar esta variavel de ambiente no seu bash para que seja impresso corretamente os pontos flutuantes L_C_NUMERIC=en_US.UTF-8

```bash
$ printf "Resolva a equação:  %d + %f = X\n" $inteiro $decimal	
```
<img src=/images/printf-output4.png title=""></img>
# Especificadores de conversão
|Caractere(s)|Tipo|
|:---:|:--|
|__%d__, __%i__|O argumento é convertido para um valor inteiro. Se houver alguma precisão especificada, a saída do comando deverá mostrar o valor na mesma quantidade de caracteres, caso tenha um zero na frente do valor numérico, a saída mostrará o valor preenchido com zeros à esquerda. A precisão padrão é 1.|
|__%o__, __%u__, __%x__, __%X__|Converte o argumento para o correspondente em octal __(o)__, decimal __(u)__, ou hexadecimal __(x__ e __X)__.|
|__%e__, __%E__|Converte e arredonda o argumento para um valor __double__ com o formato [-]d.ddde+dd. Uma conversão __%E__ usa o __E__ maiúsculo (ao invés do __e__) para introduzir um expoente. o expoente sempre contém no mínimo dois digitos; se o valor for zero, o expoente será 00.|
|__%f__, __%F__|O argumento __double__ é arredondado e convertido para notação decimal no formato [-]ddd.ddd|
|__%g__, __%G__|O argumento __double__ é convertido no estilo de __f__ ou __e__|
|__%a__, __%A__|Converte o argumento __double__ para notação hexadecimal usando letras no estilo [-]0xh.hhhhp|
|__%c__|Se não houver um modificador __l__ presente, o argumento __inteiro__ é convertido para um caracter|
|__%s__|Se não houver um modificador __l__, converte o argumento em um vetor de caracteres (string)|
|__%%__|Um '__%__' é impresso. Nenhum argumento é convertido.|

# Caracteres Bandeira
O caractere __%__ é seguido por zero ou mais das seguintes flags.  

|Flag|Descrição|
|:---:|:---|
|__#__ |(números) O valor será convertido para que contenha a quantidade de caracteres definida neste número.|
|__0__ |O valor será precedido por zeros ao invés de espaços em branco, se as flags __0__ e __-__ aparecerem juntas __0__ será ignorado.|
|__-__ |O valor convertido será alinhado à esquerda do campo delimitado (o padrão é alinhado à direita)|
|__' '__ |(um espaço) um espaço em branco deve ser deixado antes de um número positivo (ou uma string vazia)|
|__+__ |Um sinal (__+__ ou __-__) deve ser sempre colocado antes de um número produzido por conversão de sinais. Por padrão um sinal é usado apenas para números negativos. Um __+__ sobrescreve um espaço se ambos forem usados.|


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


Para mais informações sobre o comando _printf_, visite a documentação oficial em: [https://www.gnu.org/software/coreutils/printf](https://www.gnu.org/software/coreutils/printf)  
Você também pode digitar o seguinte comando diretamente do seu terminal:  
`info '(coreutils) printf invocation'`
