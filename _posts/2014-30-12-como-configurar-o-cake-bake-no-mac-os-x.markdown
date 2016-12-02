---
layout: post
title:  "Como configurar o Cake Bake no Mac OS X!"
date:   2013-12-30 17:02:06 -0200
categories: bake mac
author: 'Reinaldo Ferro'
author_url: 'https://github.com/rfoshttp://www.webdevbr.com.br'
author_url_label: 'Github'
comments: true
---
Quem está iniciando o desenvolvimento com CakePHP já deve ter ouvido muito falar do comando "cake baker" então vamos esclarecer como configurar esse comando para funcionar no seu terminal, caso você use Max OS X (Mavericks).

É uma tarefa muito simples que porém vai te ajudar muito na hora de desenvolver a base da sua aplicação, ou pelos menos vai ajudar muito na criação das tarefas mais básicas e você não vai precisar o código das funções toda vez que precisar criar uma aplicação nova. Economia de tempo é a palavra chave para o cake bake.<!--more-->

No Mac OSX cada usuário tem o seu próprio perfil no sistema e dentro do perfil temos um arquivo chamado: .profile
Esse arquivo é um arquivo de sistema e não pode ser visualizado pelo Finder como se fosse um arquivo qualquer.

Neste exemplo vou usar o editor <a href="https://panic.com/coda/" target="_blank">Coda</a> para facilitar nossa vida.

Então vamos lá... mãos à obra.

<ul>
    <li>Com o editor aberto, navegue até a pasta raiz do seu usuário, se você só conseguir visualizar pastas e nenhum arquivo, verifique nas opções "View" e habilite a função "Show Invisible File". Pronto, agora você vai visualizar todos os arquivos dentro da pasta do seu perfil.</li>
    <li>Localize o arquivo .profile e abra esse arquivo. Cuidado para não excluir informações já existentes no seu arquivo.</li>
    <li>Dentro do arquivo você precisa informar o caminho de instalação do PHP e o caminho da sua instalação do CakePHP.</li>
</ul>

Note que é uma única linha, com todas as informações separadas apenas por : (dois pontos), você não precisa separar essa configuração em várias linhas.

<pre>export PATH=/Applications/MAMP/Library/bin:/Applications/MAMP/bin/php/php5.5.10/bin:/Users/Rey/Sites/<em>cakephp</em>/app/Console:/opt/local/bin:/opt/local/sbin:$PATH</pre>

Observe que eu informei:

<pre>/Applications/MAMP/bin/php/php5.5.10/bin</pre>

e

<pre>/Users/Rey/Sites/<em>cakephp</em>/app/Console</pre>

<em>cakephp</em> é o diretório da minha aplicação

São os dois caminhos fundamentais para o Cake Bake funcionar.

Quando você concluir as alterações salve o arquivo, feche o editor de texto e feche também todas as janelas de terminal que você estiver usando naquele momento, pois as alterações só serão válidas depois que o Terminal for reaberto.

Neste exemplo estou passando as informações para quem usa o OS X e o MAMP Pro, mas existe também a versão <a href="http://www.mamp.info/" target="_blank">MAMP</a> que é gratuita para quem não quer pagar pela versão PRO do aplicativo.