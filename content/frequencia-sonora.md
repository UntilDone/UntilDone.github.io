+++
title = "Frequência Sonora"
date = 2021-04-30
updated = 2021-04-30
description = "Frequência Sonora"
draft = false

[taxonomies]
categories = ["Música"]
tags = ["música", "python", "C"]

[extra]
image = "https://upload.wikimedia.org/wikibooks/zh/0/06/Firefox.svg"
author = "Rômulo"
+++

# Introdução

Vamos usar como referência a escala de temperamento igual, onde a afinação tem como base o Lá na quarta oitava que vibra na frequência de 440 Hz (A4 = 440.00)

> Isso significa que se tocarmos esse Lá no violão, a corda vibrará 440 vezes por segundo.

Se multiplicarmos essa frequência por 2, vamos encontrar o A5 = 880.00. Que nada mais é que oito notas da escala maior acima do lá mencionado (uma oitava acima). Entre essas oitavas existem 12 notas com intervalos de semitons entre elas.  Na música isso é chamado de escala cromática.

> note que existe diferença entre escala maior e escala cromática

Em uma escala cromática de dó ascendente por exemplo, encontramos as seguintes notas:  
C - C# - D - D# - E - F - F# - G - G# - A - A# - B

Para encontrarmos a frequência da nota acima do A4 podemos usar a fórmula:  
A#4 = A4 * 2<sup>1/12</sup>  

A mesma lógica pode ser aplicada para encontrarmos notas abaixo do A4:  
F = A4 * 2<sup>-4/12</sup> (onde F é 4 semitons abaixo de A4)

# Limites da audição humana
O ouvido humano é capaz de captar frequências de som entre 16 e 20.000 (hz)
Como a nota mais baixa que conseguimos ouvir é o C0 = 16(hz), podemos utilizá-lo na nossa fórmula para encontrar a tonalidade de uma determinada frequência. Uma tabela com as frequencias sonoras pode ser encontrada em [https://pages.mtu.edu/~suits/notefreqs.html](https://pages.mtu.edu/~suits/notefreqs.html)

# Matemática

Para uma tonalidade T, o número de semitons de C0 até T é:

s = 12 log<sub>2</sub>(T / C0)

# Algoritmo

Trecho de um código em python que calcula o número de semitons de C0 até uma frequência, e então computa a tonalidade correspondente:

```python
from math import log2, pow


A4 = 440
C0 = A4*pow(2, -4-9/12)
sigla = ["C", "C#", "D", "D#", "E", "F", "F#", "G", "G#", "A", "A#", "B"]

def tom(frequencia):
    semiton = round(12*log2(frequencia/C0))
    oitava = semiton // 12
    nota = semiton % 12
    return f"{sigla[nota]}{str(oitava)}"

```

O mesmo algoritmo traduzido para C:
```C
#include <math.h>
#include <stdio.h>
#include <stdlib.h>

int tom(double frequencia)
{
	double A4 = 440;
	double C0 = A4 * pow(2, -4.75);
	char* sigla[12] = {"C", "C#", "D", "D#", "E", "F", "F#", "G", "G#", "A", "A#", "B"};

	double semitons = round(12*log2(frequencia/C0));
	int oitava = semitons / 12;
	int nota = (int) semitons % 12;

	printf("%s%d\n", sigla[nota], oitava);

	return 0;
}

```
O tom A4 possui sua propria variável para caso você precise modificar o código para uma afinação diferente.

Crédito do trecho em python: [https://www.johndcook.com/blog/2016/02/10/musical-pitch-notation/](https://www.johndcook.com/blog/2016/02/10/musical-pitch-notation/)
