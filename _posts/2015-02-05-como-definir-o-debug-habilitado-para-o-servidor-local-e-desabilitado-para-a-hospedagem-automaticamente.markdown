---
layout: post
title:  "Como definir o debug habilitado para o servidor local e desabilitado para a hospedagem automaticamente"
date:   2015-02-05 12:40:06 -0200
categories: deploy
author: 'Andre Cavallari'
comments: true
---

Este post está destinado a pessoas que vêm me perguntando se existe uma forma de o Cake identificar automaticamente se o servidor é o de desenvolvimento ou de produção, e configurar o debug automaticamente conforme o tipo de servidor.

Bom, sabemos que para quem desenvolve, é imprescindível o uso do debug, mas o mesmo deve ser desativado ao público, porém algumas vezes precisamos estar constantemente alterando diretrizes no core.php (ou no app.php no caso do Cake 3.0), e se enviarmos este arquivo para o servidor de produção podemos estar sem querer habilitando o debug na produção, o que é uma falha grave. Mas podemos automatizar o processo do debug e configurá-lo conforme o servidor, para isto existem várias opções.<!--more-->

<hr />

&nbsp;
<h3><strong>1. Minha preferida, utilizar um arquivo de configuração global do PHP</strong></h3>
O php.ini tem uma diretriz chamada "auto_prepend_file", esta diretriz define que um arquivo.php será sempre adicionado ao qualquer projeto que você criar com PHP, o mesmo será SEMPRE adicionado no início de qualquer script PHP. Para proceder...
<ol>
	<li>Abra o php.ini e procure a linha "auto_prepend_file" e altere para "auto_prepend_file=/caminho/para/global_config.php" por exemplo, (C:\caminho\para\global_config.php no windows), este global_config.php pode estar em qualquer pasta.</li>
	<li>Crie o arquivo global_config.php na pasta definida no php.ini</li>
	<li>Insira o código abaixo
&lt;?PHP
define('CAKE_DEBUG',2);
OU... caso trabalhe com Cake 2.x e Cake 3.0 no mesmo servidor utilize:
define('CAKE2_DEBUG,2);
define('CAKE3_DEBUG,1);</li>
	<li>Reinicie o apache</li>
	<li>abra o arquivo core.php (no cake 2.x) procure pela linha "Configure::write('debug',2);" e altere para "Configure::write('debug',0);" e logo abaixo desta linha insira:
if(defined('CAKE2_DEBUG')) Configure::write('debug',CAKE_DEBUG);</li>
	<li>No Cake 3.0 você insere no final do código:
if(defined('CAKE3_DEBUG')) $config['debug'] = CAKE3_DEBUG;</li>
</ol>
Pronto, agora pode alterar o core.php ou app.php a vontade e enviar para o servidor de produção quando quiser que não correrá mais o risco de habilitar o debug sem querer no servidor de produção...
<h3><strong>2ª opção: Utilizando o SetEvent no Apache.</strong></h3>
Uma outra opção é utilizar a diretriz SetEnv do Apache, assim terá a diretriz env('CAKE2_DEBUG') na aplicação no servidor de desenvolvimento, e não no de produção.
<ol>
	<li>Abra o httpd.conf e insira em qualquer lugar o código:
SetEnv CAKE2_DEBUG 2
SetEnv CAKE3_DEBUG 1</li>
	<li>Salve o httpd.conf e reinicie o apache</li>
	<li>Abra o core.php da sua aplicação e modifique a linha "Configure::write('debug',2)" para 0, e logo abaixo insira:
if(env('CAKE2_DEBUG')) Configure::write('debug',env('CAKE2_DEBUG'));</li>
	<li>No Cake 3.0 insira no final do app.php:
if(env('CAKE2_DEBUG')) $config['debug'] = env('CAKE3_DEBUG');</li>
</ol>
Existe também a possibilidade de alterar o .htaccess da sua aplicação inserindo a diretriz SetEnv, mas todo novo projeto terá que alterar o .htaccess (Lembre-se, sempre o do webroot), inserindo direto no httpd.conf você terá essas opções globais, porém toda vez que precisar alterar terá que reiniciar o apache.
<h3><strong>3ª Opção: Identificando o servidor local</strong></h3>
Esta solução foi sugerido por um usuário do grupo do facebook, então estarei postando aqui também.
<ol>
	<li>Abra o arquivo core.php e insira as seguintes linhas:
<span class="UFICommentBody">if (env('SERVER_ADDR') == '127.0.0.1' ||
strstr(env('SERVER_NAME'), 'dev') !== false ||
strstr(env('SERVER_NAME'), 'localhost') !== false ||
// C0A8 stands for IPv6 Address
strstr(env('SERVER_ADDR'), 'C0A8') !== false ||
strstr(env('SERVER_ADDR'), '192.168') !== false
) {
Configure::write('debug', 2);
} else {
Configure::write('debug', 0);
}</span></li>
</ol>
<h3><strong>Conclusão</strong></h3>
As três opções listadas aqui vão trazer um resultado satisfatório, particularmente prefiro a primeira opção, pois você pode alterar o debug através do arquivo de configuração global a qualquer momento sem a necessidade de reiniciar o apache para surtir efeito. A segunda opção é uma sugestão dos mantenedores do Cake, gosto muido desta opção também porém toda vez que precisar alterar a diretriz terá que reiniciar o apache (Exceto no caso de utilizar o .htaccess, aí não será necessário reiniciar, mas se ocorrer de sem querer enviar para produção o .htaccess, estará habilitando o debug ao público).