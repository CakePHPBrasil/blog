---
layout: post
title:  "CakePHP - Rotas - Transformar /users em /usuarios"
date:   2017-03-02 15:05:00 -0200
categories: rotas
author: Maicon Pinto
author_url: 'http://github.com/maiconpinto'
author_url_label: 'Maicon Pinto'
comments: true
---

## Documentação

[Routing](https://book.cakephp.org/3.0/en/development/routing.html)

## Desafio

Trasnformar as rotas `/users` em `/usuarios`.

## Solução

```php
// config/routes.php

$routes->connect('/usuarios', ['controller' => 'Users']);
$routes->connect('/usuarios/:action', ['controller' => 'Users']);
$routes->connect('/usuarios/:action/*', ['controller' => 'Users']);
```

## Explicação

A rota `/usuarios` servirá para quando o usuário digitar apenas `/usuarios`. Mas, se tivesse apenas esta rota, você não conseguiria acessar a url `/usuarios/add`, pois retornaria um erro que não foi encontrado o **UsuariosController**.
Isso aconteceria, pois as actions não estão mapeadas, para isso, há a segunda rota `/usuarios/:action`.
Assim, qualquer action fica coberta por esta rota. Exemplos:

- `/users/login` => `/usuarios/login`
- `/users/logout` => `/usuarios/logout`

Se você não tivesse urls passando parâmetros, como `/usuarios/view/1`, só a primeira e segunda rotas, já estaria ok.
Mas, urls como da view, ainda não estão funcionando.
Por isso, usa-se um coringa '*', para dizer que qualquer coisa depois da action fosse redirecionada para o controller Users, e action correspondente.

Bom, essa foi a dica de hoje. Para quem está acostumado a utilizar o CakePHP, esse tutorial é bem básico, mas para quem está começando, deve ajudar.

Eu não estou acostumado a escrever, por isso, prefiro encurtar as palavras e não enrolar muito.

Caso tenha ficado alguma dúvida, ou tenha outra solução, fique a vontade para deixar seu comentário, ou criar um PR com seu artigo, tenho certeza que a comunidade agradece.