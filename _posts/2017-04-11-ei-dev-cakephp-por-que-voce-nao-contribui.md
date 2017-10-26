---
layout: post
title:  "Ei, Dev Cakephp. Por que você não contribui?"
header-img: "assets/img/post-bg-05.jpg"
date:   2017-04-11 00:04:00 -0200
categories: documentacao
author: 'Alan Lira'
author_url: 'https://github.com/lira92'
author_url_label: 'Github'
comments: true
---

## Ei, Dev Cakephp. Por que você não contribui? ##

Apesar do título um pouco polêmico, este artigo não terá nada de polêmico, o motivo de eu estar escrevendo-o é que acredito que seja um objetivo comum de um desenvolvedor quando aprende uma linguagem, framework ou uma lib, contribuir pro crescimento dos mesmos, e muitas vezes ficamos tentando desenvolver uma feature enorme ou corrigir um bug relatado e acabamos sendo desmotivados porque aquilo parece muito complexo. 

Vou citar o exemplo do framework cakephp 3, que utilizo com mais frequência,  ele possui uma documentação que descreve os recursos do framework que tem o nome de cookbook, a qual possui suporte para vários idiomas. O problema é que a documentação completa e atualizada é somente em inglês, dependendo que integrantes da comunidade submetam as traduções.

Há algum tempo comecei a ficar incomodado, pois em todas as vezes que eu procurava algo sobre o cakephp no google ele me direcionava para o cookbook, o idioma que vinha pré-definido era o português, e praticamente todas as vezes a imagem que aparecia era esta:

![enter image description here](http://ap.imagensbrasil.org/images/2017/04/09/Selecao_065.png)

Todas as vezes eu alterava o idioma para o inglês, e por mais que o meu inglês não seja dos melhores, eu conseguia ler e entender para resolver meu problema. A alguns dias quando eu fiz isso novamente, eu analisei minha ação e pensei, se alguma pessoa que está querendo aprender cakephp e entra em uma página que não tem suporte a português com certeza a dificuldade dela aprendê-lo será ainda maior, caso não tenha inglês fluente, pois além de entender como as coisas no cakephp funcionam, terá que ficar dependendo do google tradutor. 

Foi então que cogitei começar a contribuir para a tradução de algumas páginas da documentação e mudar um pouco essa situação, e me surpreendi com o resultado, pois, durante a leitura minuciosa da documentação em inglês, eu acabei descobrindo coisas que eu não utilizava do framework ou utilizava erroneamente, além é claro, de dar uma exercitada no idioma inglês, que por sinal, se você é da área de tecnologia não preciso explicar porque isso é importante, certo? risos. 

Recordando o assunto levantado no início deste artigo, sobre o interesse em contribuir, essa é a minha dica para você desenvolvedor cakephp, contribua para a tradução do cookbook! Você não precisará de super poderes para ajudar, e ainda o seu conhecimento só tem a crescer, tanto no idioma quanto no framework.

#Por onde começar#

Se você está interessado em contribuir com as traduções, há algumas coisas que são interessantes para saber antes de contribuir:

 1. A documentação é mantida no github, neste [repositório](https://github.com/cakephp/docs). Para submeter você deve criar um fork, alterar a página desejada e submeter um pull request.
 2. A documentação é escrita em [reStructuredText](https://pt.wikipedia.org/wiki/ReStructuredText), uma linguagem de marcação nos moldes do Markdown. [Aqui](http://www.sphinx-doc.org/pt_BR/stable/rest.html) você pode ler mais sobre ele.
 3. A documentação do cakephp usa o Travis CI para integração contínua e quando você enviar um pull request, se atenha ao resultado da build, ela é executada para gerar o html através dos arquivos .rst (extensão reStructuredText).

#Páginas traduzidas por mim#

Desde que decidi começar a contribuir com as traduções, eu traduzi as páginas abaixo da documentação para pt-br:

 - [Views](https://book.cakephp.org/3.0/pt/views.html)
 - [View Cells](https://book.cakephp.org/3.0/pt/views/cells.html)
 - [Temas](https://book.cakephp.org/3.0/pt/views/themes.html)

Se você encontrou algum problema nas minhas traduções, por favor, submeta um pull request para o repositório oficial com a correção. Você já contribuiu com a tradução/correção de alguma página do cookbook? Existe alguma página muito importante do cookbook que não possui tradução para pt-br? Deixe seu comentário!
