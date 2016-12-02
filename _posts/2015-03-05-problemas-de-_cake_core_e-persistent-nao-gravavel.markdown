---
layout: post
title:  "Problemas de _cake_core_ e persistent não gravável"
date:   2015-03-05 12:40:06 -0200
categories: permissao
author: 'Leonardo Siervo Belini'
comments: true
---
Um problema que pode ser muito comum no Fedora é do" <strong>_cake_core_ </strong>..." e do "<strong>... persistent is not writable ...</strong>":

<hr />

<!--more-->

<b>Warning</b>: _cake_core_ cache was unable to write 'cake_dev_pt-br' to File cache in <b>/var/www/html/cakeBlog/lib/Cake/Cache/Cache.php</b> on line <b>310</b>

<b>Warning</b>: /var/www/html/cakeBlog/app/tmp/cache/persistent/ is not writable in <b>/var/www/html/cakeBlog/lib/Cake/Cache/Engine/FileEngine.php</b> on line <b>337</b>

<b>Fatal error</b>: Uncaught exception 'CacheException' with message 'Cache engine _cake_core_ is not properly configured.' in /var/www/html/cakeBlog/lib/Cake/Cache/Cache.php:166 Stack trace: #0 /var/www/html/cakeBlog/lib/Cake/Cache/Cache.php(136): Cache::_buildEngine('_cake_core_') #1 /var/www/html/cakeBlog/app/Config/core.php(336): Cache::config('_cake_core_', Array) #2 /var/www/html/cakeBlog/lib/Cake/Core/Configure.php(78): include('/var/www/html/c...') #3 /var/www/html/cakeBlog/lib/Cake/bootstrap.php(171): Configure::bootstrap(true) #4 /var/www/html/cakeBlog/app/webroot/index.php(92): include('/var/www/html/c...') #5 {main} thrown in <b>/var/www/html/cakeBlog/lib/Cake/Cache/Cache.php</b> on line <b>166</b>

<hr />

Para resolver esse problema é muito simples:
<ol>
	<li>Abre o terminal e execute o seguinte comando (no meu caso usarei o gedit, você pode usar qualquer um de sua preferencia):
<ol>
	<li><em>sudo gedit /etc/selinux/config</em></li>
</ol>
</li>
	<li>Procure a linha <strong>SELINUX</strong>.</li>
	<li>Altera para <strong>disabled</strong>, ficando assim: <strong>SELINUX=disabled</strong></li>
	<li>Após isso salve e reinicie o computador.</li>
	<li>Agora é só colocar as permissões nos arquivos do CakePHP que irá funcionar normalmente.</li>
</ol>
Link de onde o tutorial foi baseado: <a href="https://groups.google.com/forum/#!topic/cake-php/ULapxcvVIbs" target="_blank">Aqui</a>

&nbsp;