+++
title = "Rastrear mensagens de erro no Bash"
description = "Relata como descobriu o comando bash -x e explica como ele pode ser útil."
date = 2021-03-26
thumbnail = "https://upload.wikimedia.org/wikipedia/commons/thumb/4/4b/Bash_Logo_Colored.svg/512px-Bash_Logo_Colored.svg.png"
tags = ["Bash", "troubleshooting", "cat", "grep", "wc"]

[extra]
author = "Rômulo Pinheiro"
paginate_by = 5
+++

Estou na linha de comando quando me deparo com uma mensagem de erro. Mas infelizmente não existe referência para o arquivo de origem nesta mensagem. E o que encontrei na internet foram artigos bem genéricos sobre o problema, e agora? Neste artigo compartilho alguns comandos que utilizei pra resolver este impasse. Segue abaixo a mensagem:

``` 
bash: eval: linha 335: encontrado EOF inesperado enquanto procurava por `'' correspondente
bash: eval: linha 336: erro de sintaxe: fim prematuro do arquivo
```

Aqui observamos que o problema se encontra entre a linha 335 e 336 de algum arquivo. Trata-se de um erro de sintaxe, e o script em questão não foi executado até o fim como descrito acima.

Mas para compreender melhor do que se trata, é necessário ficar atento no contexto. O que eu estava fazendo no momento que a mensagem surgiu? Bom. esta mensagem surge todas as vezes que eu abro o terminal. Isso significa que está relacionada com algum arquivo que é executado na inicialização do terminal? Vamos descobrir.

O arquivo _.bashrc_ é o responsável por executar as configurações que serão inicializadas com o terminal.Ele fica localizado na pasta _/home/usuário/_. Porém no meu caso, este arquivo não chega a ter nem 300 linhas. E podemos observar isso com o seguinte comando:

```bash
$ wc -l /home/usuario/.bashrc
80 .bashrc
```

Ocorre que este arquivo importa configurações de outros arquivos. com o comando _source_. Vamos descobrir que arquivos são estes.

```bash
$ cat .bashrc | grep "source"
source "$BASH_IT"/bash_it.sh
source "$ZZPATH"
```

Agora vamos verificar quantas linhas todos esses arquivos possuem juntos.

```bash
$ wc -l .bashrc .bash_it/bash_it.sh /usr/local/bin/funcoeszz
    80 .bashrc
   159 .bash_it/bash_it.sh
 20551 /usr/local/bin/funcoeszz
 20790 total
```

Mais de 20 mil linhas. Então é sim possível que a mensagem de erro esteja em algum lugar entre elas. Mas são muitas linhas, e agora? Será que existe alguma forma de rastrear o processo de execução desse arquivo? A resposta é sim. Existe uma forma de coletar os passos de execução de um script linha por linha com uma opção do bash:  
```bash -x .nomedoscript.sh```

Quando executei esse comando aqui. me retornou um monte de linhas no prompt. Para facilitar a vida, é possível redirecionar essa saída para outro arquivo. Vamos fazer isso com:

```bash
bash -x .bashrc 2> log
```

Aqui nós redirecionamos as mensagens de erro para um novo arquivo chamado _log_. Agora é só buscarmos dentro desse arquivo aquilo que estiver em torno das linhas citadas lá no inicio. Vamos testar:

```bash
$ cat -n log | head -338 | tail -15 

   324	++++ cut -d . -f 2
   325	+++ extension=aliases
   326	+++ BASH_IT_LOG_PREFIX='aliases: fuck: '
   327	+++ _log_debug 'Loading component...'
   328	+++ about 'log a debug message by echoing to the screen. needs BASH_IT_LOG_LEVEL >= BASH_IT_LOG_LEVEL_ALL'
   329	+++ :
   330	+++ param '1: message to log'
   331	+++ :
   332	+++ example '$ _log_debug "Loading plugin git..."'
   333	+++ :
   334	+++ group log
   335	+++ :
   336	+++ [[ '' -ge 3 ]]
   337	+++ return 0
   338	+++ source /home/romulo/.bash_it/enabled/150---fuck.aliases.bash

```
> **Cat** com a opção **-n** enumera tudo que estiver em **log** linha por linha. E com um _pipe_ ``` | ``` podemos redirecionar a saída do **cat** para o **head** que nos retorna apenas as primeiras linhas que estiverem seguidas do hífen ```-338```. Com mais um **pipe** redirecionamos tudo que for retornado até agora para o **tail** que nos retorna apenas as últimas linhas também definidas com um hífen ```-15```.

De acordo com esse trecho, dá pra ver que meu problema está relacionado com uma condição que faz uma avaliação numérica com uma string vazia ```[[ '' -ge 3 ]]```. Também podemos observar que o trecho do código está relacionado com um plugin chamado BASH_IT. 

Depois de desinstalar o plugin meu terminal voltou ao normal. E aprendi que o bash já está cheio de recursos que nos ajudam a resolver nossos problemas no terminal. Basta dar uma olhada no manual do Bash. 
