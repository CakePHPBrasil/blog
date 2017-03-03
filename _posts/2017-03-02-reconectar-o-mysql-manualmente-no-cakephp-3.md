---
layout: post
title: "Reconectar o MySQL manualmente no CakePHP 3"
date: 2017-03-02 21:40:00
categories: dicas
author: Flaviano Honorato
author_url: 'http://flaviano.com.br'
author_url_label: 'http://flaviano.com.br'
comments: true
---


## O Erro
Desenvolvemos um sistema para gerar relatórios em algumas partes de nossa aplicação. O processo estava rodando com uma longa execução via terminal(shell CakePHP). Tivemos problemas estranhos após a implantação da fila para o servidor de produção. Algumas rotinas foram processadas perfeitamente no início, mas depois de um dia, todos os trabalhos de relatório falharam. Se nós reiniciar-mos a fila, eles voltam a funcionar normalmente, e então depois de um dia voltam a falhar.

No arquivo de log, encontramos algumas mensagens de erro como essa abaixo:

```sh
Exception: SQLState[HY000]: General error: 2006 MySQL server has
 gone away in [xxx/vendor/cakephp/cakephp/src/Database
/Statement/MysqlStatement.php line 36]
```
O erro acima indica que tem algo a ver com a parte do banco de dados do nosso sistema.

## Primeira tentativa

Como você deve ter imaginado, nossa primeira tentativa é tentar encontrar respostas no Google. Todos os links na primeira página do Google nos dizem que precisamos aumentar os valores para **max_allowed_packet** e **wait_timeout**.

No entanto, nada funcionou após a atualização desses valores.


## Solução

Passamos dias tentando encontrar a causa do problema. Tínhamos a certeza que seria algo relacionado com a ligação com a base de dados. Nós não tivemos nenhuma idéia do que poderia estar ocasionando isso, até que nós lemos o código fonte do CakePHP 3. Há um ingresso no repositório do CakePHP 3 indicando que ele não reconecta automaticamente no MySQL se ele falhar [https://github.com/cakephp/cakephp/issues/3423](https://github.com/cakephp/cakephp/issues/3423).

Finalmente percebemos a causa:

Uma vez que iniciamos nosso shell no CakePHP, ele usa uma única instãncia da conexão com o banco de dados até que o processo seja encerrado. Nosso processo de execução de shell do CakePHP é longo, e, uma vez que é iniciado, ele nunca será desligado de propósito. Se nenhum processo for enviado, a conexão MySQL se manterá aberta e permanecerá ociosa. Quando isso é maior que o **wait_timeout**, a exceção é lançada.

Podemos ajustar a configuração do **wait_timeout**. Mas não podemos configurá-lo para ficar para sempre. Precisamos de uma solução melhor.

A solução é re-conectar MySQL se uma exceção é lançada. Para fazer isso, podemos simplesmente adicionar apenas três linhas como mostrado abaixo:

```php 
<?php
use Cake\Datasource\ConnectionManager;

$connection = ConnectionManager::get('default');
$connection->disconnect();
$connection->connect();
```

Documentação: [https://book.cakephp.org/3.0/en/orm/database-basics.html#database-basics](https://book.cakephp.org/3.0/en/orm/database-basics.html#database-basics)

## Conclusão

Esperemos que este tutorial simples ajude você com o seu desenvolvimento, essa é uma dica bem básica mas que pode salvar vidas (risos).

Se você tiver dúvidas ou encontrar nossos erros no tutorial acima, deixe um comentário abaixo para nos informar.

Post originalmente publicado em [outro blog](https://www.startutorial.com/articles/view/manually-reconnect-mysql-in-cakephp-3), fizemos apenas a tradução e adaptamos algumas coisas para melhor entendimento.

Caso tenha ficado alguma dúvida, ou tenha outra solução, fique a vontade para deixar seu comentário, ou criar um PR com seu artigo, tenho certeza que a comunidade agradece.