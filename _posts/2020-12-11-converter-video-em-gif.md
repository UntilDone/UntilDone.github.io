---
layout: post
title: Como converter video em gif 
date: 2020-12-11
categories: Bash
published: true
---

Estava fazendo uns ajustes no meu blog, quando de repente o plugin da ferramenta que uso pra editar meus códigos mostrou um erro na tela. Resolvi então fazer uma pausa e reportar o bug no repositório dos desenvolvedores do plugin. Conforme eu preenchia o formulário, percebi que demonstrar o problema com um gif ao invés de vários screenshots seria mais eficiente.

A maneira mais conveniente que me veio em mente foi fazer um screencast com a ferramenta nativa do gnome, que pode ser ativada através do atalho `Ctrl` + `Alt` + `Shift` + `R`. Um círculo vermelho/laranja aparece no canto superior direito do monitor indicando que a tela está sendo gravada. Aí é só apertar `Ctrl` + `Alt` + `Shift` + `R` mais uma vez quando a gravação estiver concluída que a ferramenta joga a gravação no formato .webm direto na pasta 'Vídeos' do nosso sistema. Legal!

![gif](https://github.com/PinheiroCosta/PinheiroCosta.github.io/raw/master/_images/erro.gif)

Mas como infelizmente alguns sites não aceitam webm incorporados em suas páginas. Converter pra gif me pareceu ser uma boa opção. Para isso utilizei a ferramenta [FFmpeg](https://ffmpeg.org/). Já tinha ouvido falar dessa ferramenta mas nunca a tinha usado antes. Ela é bem versátil e me pareceu ser bastante completa, capaz de realizar toda sorte de trabalho com audio/vídeo. 

Depois de algumas instruções na página oficial e artigos que encontrei na internet, consegui elaborar um script pra fazer todo trabalho por nós. Você pode encontrar o script no meu reposiório, clicando aqui. E para usá-lo é simples, basta copiar o arquivo 'webmtogif' para o seu diretório */usr/local/bin/* e invocá-lo com o comando:
```shell
$ webmtogif nomedoarquivo.webm
```
ou
```shell
$ webmtogif caminho/do/arquivo/video.webm
```

O arquivo gif será criado na pasta de onde o script foi executado.

### **Pré requisito**
**Certifique-se de instalar a ferramenta ffmpeg antes de usar o script. Ela pode ser encontrada no do site oficial ou instalada através do seu gerenciador de pacotes.**
