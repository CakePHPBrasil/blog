---
layout: post
title:  "Instalando e configurando o CakePHP!"
date:   2015-01-07 19:46:06 -0200
categories: basico
author: 'Erik Figueiredo'
author_url: 'http://www.webdevbr.com.br'
author_url_label: 'WebDevBr'
comments: true
---

Meu primeiro artigo aqui no CakePHP Brasil é dedicado a todos os que querem iniciar no Framework, bem vindo a série Curso de Introdução ao CakePHP.

Nesta série abordaremos as duas versões mais rescentes do CakePHP, a 2 e a 3, pra isso sempre vou começar com uma introdução geral e partir para o Cake 2, na sequência eu repito o processo para o CakePHP 3.<!--more-->

Para este curso vamos precisar de um banco de dados, vou usar MySql e o meu banco vai chamar tutorial_cakephpbrasil.

Vamos lá?
<h3>Instalando o CakePHP 2</h3>
Pra começar, vá ao site oficial do CakePHP (<a href="http://cakephp.org/" target="_blank">www.cakephp.org</a>), do lado direto tem um Download vermelho bem grande, com a versão mais rescente, se neste ponto você encontrar a 3.* (* = a qualquer coisa, 3.1.2 por exemplo), então vá direto ao repositório no GitHub para baixar a versão 2 (<a href="https://github.com/cakephp/cakephp/tags" target="_blank">neste link</a>), é só rolar pra encontrar a versão 2.* mais rescente.

Com o arquivo compactado em mãos... bem, desnecessário, mas lá vai, rsrsrsrs: descompacte dentro do diretório do seu servidor web local (htdocs, www...).

Verifique se o diretório em app/tmp tem permissão de leitura e escrita (777) recursivamente (nele próprio e em todos os outros diretórios e arquivos dentro dele).

Agora abra o diretório do CakePHP no seu navegador pra ver se está tudo certo, se uma tela com alguns avisos em vermelho, verde e amarelo aparecer é porque deu tudo certo.

Vamos resolver estes alertas e deixar tudo verdinho?
<h3>Configurar o CakePHP 2</h3>
Cada cor é uma prioridade, vamos começar pelos vermelhos. Tem duas configurações de segurança que precisamos resolver, é o Security.Salt e o Security.CypherSeed, acesse o arquivo em app/Config/core.php e localize as linhas que começam como o exemplo abaixo:
<pre>Configure::write('Security.salt',...
</pre>
<pre>Configure::write('Security.cipherSeed',...
</pre>
Pronto, os vermelhinhos estão resolvidos, se tiver mais algum no seu me avisa nos comentários ou no forum.

Pra fechar, vamos acertar um amarelinho, o do Banco de dados.

Vá ao diretório app/Config e renomeie o arquivo database.php.default para database.php.

Abra ele e acerte as configurações de acesso do array $default para as do seu banco de dados:
<pre>public $default = array(
'datasource' =&gt; 'Database/Mysql',
'host' =&gt; 'localhost',
'port' =&gt; '',
'login' =&gt; 'root',
'password' =&gt; '',
'database' =&gt; 'tutorial_cakephpbrasil',
'prefix' =&gt; '',
'encoding' =&gt; 'utf8'
);</pre>
Quando você abrir o navegador deve encontrar o aviso do banco (antes amarelo) na cor verde, se não estiver confira todos os dados de conexão e poste nos comentários ou no forum, para conferir, você deve acaba com apenas uma mensagem amarela, vamos ignorar isso.

Parabéns, o CakePHP 2 está configurado.
<h3>Instalando o CakePHP 3</h3>
O CakePHP já tem um conceito muito mais moderno, então vamos aproveitar isso, pra começar garanta que você já tem o Composer acessando o site e baixando no diretório que quer instalar o CakePHP 3 (se não conhece o Composer não sabe o que está perdendo).

Não vou me aprofundar no assunto, lá tem opção para baixar via linha de comando (usando PHP ou Curl), link direto (Manual Download) e até um instalador pra Windows.

Note que você pode acabar com o composer instalado globalmente (com o instalador do Windows por exemplo) ou com ele no diretório local.

Abra a linha comando e garanta que o php roda na linha de comando com php -v, ele deve mostrar a versão do PHP.

Pra instalar o CakePHP execute o comando abaixo:
<pre>php composer.phar create-project --prefer-dist -s dev cakephp/app [app_name]</pre>
Para instalação local do composer
<pre>composer create-project --prefer-dist -s dev cakephp/app [app_name]</pre>
Para instalação global do composer

Substitua o [app_name] pelo nome do diretório que ele vai criar.

No fim verifique se os diretórios logs e tmp tem permissão de escrita e leitura (777).
<h3>Configurar o CakePHP 3</h3>
O Composer já configura o Security.Salt sozinho (o Security.CypherSeed não existe mais), falta agora configurar o banco de dados.

Localize o arquivo config/app.php e dentro dele a entrada Datasources no array $config:
<pre>config = [
    // More configuration above.
    'Datasources' =&gt; [
        'default' =&gt; [
            'className' =&gt; 'Cake\Database\Connection',
            'driver' =&gt; 'Cake\Database\Driver\Mysql',
            'persistent' =&gt; false,
            'host' =&gt; 'localhost',
            'username' =&gt; 'root',
            'password' =&gt; '',
            'database' =&gt; 'tutorial_cakephpbrasil',
            'encoding' =&gt; 'utf8',
            'timezone' =&gt; 'UTC'
        ],
    ],
];
</pre>
Pronto, o CakePHP 3 já está configurado.
<h3>Conclusão</h3>
Com o CakePHP já configurado, vamos partir pro próximo artigo, que vai mostrar a criação da nossa primeira aplicação, um gerenciador de usuários.