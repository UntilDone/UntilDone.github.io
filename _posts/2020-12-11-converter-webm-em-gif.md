---
layout: post
title: Como converter webm em gif 
date: 2020-12-11
categories: bash, gif, webm
published: true
---

Estava fazendo uns ajustes no blog, quando de repente o plugin da ferramenta do editor de códigos mostrou uma mensagem de erro na tela. Resolvi então fazer uma pausa e reportar o bug no repositório dos desenvolvedores do plugin. Conforme eu preenchia o formulário, percebi que demonstrar o problema com um gif ao invés de várias imagens seria mais eficiente.

A maneira mais conveniente que me veio em mente foi fazer um screencast com a ferramenta nativa do gnome, que pode ser ativada através do atalho `Ctrl` + `Alt` + `Shift` + `R`. Um círculo vermelho/laranja aparece no canto superior direito do monitor indicando que a tela está sendo gravada. Aí é só apertar `Ctrl` + `Alt` + `Shift` + `R` mais uma vez quando a gravação estiver concluída que a ferramenta joga a gravação no formato .webm direto na pasta 'Vídeos' do nosso sistema. Legal!

![gif](https://github.com/PinheiroCosta/PinheiroCosta.github.io/raw/master/_images/erro.gif)

Mas como infelizmente alguns sites não aceitam webm incorporados em suas páginas. Converter pra gif me pareceu ser uma boa opção. Para isso utilizei a ferramenta [FFmpeg](https://ffmpeg.org/). Já tinha ouvido falar dessa ferramenta mas nunca a tinha usado antes. Ela é bastante versátil e me pareceu ser bem completa, capaz de realizar toda sorte de trabalhos com audio e vídeo. 

Depois de ler algumas instruções na página oficial e artigos que encontrei na internet, consegui elaborar um script pra fazer todo trabalho por nós. Você pode encontrar o script no meu reposiório, [clicando aqui](https://github.com/PinheiroCosta/webmtogif). E para usá-lo é simples, basta executar o arquivo *webmtogif* usando o nome do arquivo como parâmetro:
```shell
$ bash webmtogif nomedoarquivo.webm
```
ou
```shell
$ bash webmtogif caminho/do/arquivo/video.webm
```

Para facilitar nossa vida, é possível tornar o arquivo executavel e chamá-lo diretamente
```shell
chmod +x webmtogif
./webmtogif arquivodevideo.webm
```

O arquivo gif será criado na pasta de onde o script foi executado.

>Certifique-se de instalar a ferramenta ffmpeg antes de usar o script. Ela pode ser encontrada no [site oficial](https://ffmpeg.org/) ou instalada através do seu gerenciador de pacotes.

E o plugin? Ah, depois de reportar o problema, o responsável da ferramenta me lembrou de que nem toda mensagem de erro na tela é um bug. O problema estava na minha máquina. :joy:
