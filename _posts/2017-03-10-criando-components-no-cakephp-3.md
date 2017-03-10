---
layout: post
title: "Criando Components no CakePHP 3"
date: 2017-03-07 10:20:00
categories: tutorial
author: Flaviano Honorato
author_url: 'http://flaviano.com.br'
author_url_label: 'http://flaviano.com.br'
comments: true
---


## O que é um Component segundo a doc do CakePHP

Os componentes são pacotes de lógica que são compartilhados entre controllers. O CakePHP vem com um conjunto fantástico de componentes que você pode usar para ajudar em várias tarefas comuns. Você também pode criar seus próprios componentes. Se você achar precisa copiar e colar coisas entre controllers, você deve considerar criar seu próprio Component para conter a funcionalidade. A criação de Components mantém o código dos controllers mais limpos e permite que você reutilize código entre controllers diferentes.

Documentação: [https://book.cakephp.org/3.0/en/controllers/components.html#components](https://book.cakephp.org/3.0/en/controllers/components.html#components)

## Criando um Component

Para nosso exemplo vamos criar um Component para criação de senhas com caracteres aleatórios. Para isso precisamos criar uma classe no diretório `src/Controller/Component/`, um nome de component seguindo a convenção DO cake seria algo como: `MinhaClasseComponent.php` que extend da classe `Component`.
Como umas das filosofias do nosso Framework favorito é facilitar o trabalho, podemos usar o PHP CLI(command line inteface) ou vulgarmente conhecido como Bake.

Para executar o cake, precisamos simplesmente executar o código abaixo.
```sh
bin/cake
```
Com esse comando teremos uma saída no terminal parecido com isso:

```sh
Welcome to CakePHP v3.3.14 Console
---------------------------------------------------------
App : src
Path: /var/www/cakephp.dev/src/
PHP: 7.0.16
---------------------------------------------------------
Current Paths:
App: src
Path: /var/www/cakephp.dev/src
Core: /var/www/cakephp.dev/vendor/cakephp/cakephp

Available Shells:

[Bake] bake

[DebugKit] benchmark, whitespace

[Migrations] migrations

[CORE] cache, i18n, orm_cache, plugin, routes, server

[app] console

To run an app or core command, type `cake shell_name [args]`
To run a plugin command, type `cake Plugin.shell_name [args]`
To get help on a specific command, type `cake shell_name --help`

```

Note que o nosso shell do cake nos oferece algumas possibilidades para geraçao de código, debug, migrations e etc, a possibilidade é infinita.

No nosso caso usaremos o `bake`, agora se executarmos o seguinte código:
```sh
bin/cake bake
```

Teremos a seguinte saída no nosso terminal:

```sh
Welcome to CakePHP v3.3.14 Console
---------------------------------------------------------------
App : src
Path: /var/www/cakephp.dev/src/
PHP : 7.0.16
---------------------------------------------------------------
The following commands can be used to generate skeleton code for your application.

Available bake commands:

- all
- behavior
- cell
- component
- controller
- fixture
- form
- helper
- mailer
- migration
- migration_diff
- migration_snapshot
- model
- plugin
- seed
- shell
- shell_helper
- task
- template
- test

By using `cake bake [name]` you can invoke a specific bake task.

```

Note que as possibilidades aumentaram, e podemos gerar códigos para controller, models, plugins, inclusive executar consultar no próprio shell.

Finalmente vamos criar nosso component(risos), este foi uma pequena introcução ao shell do cakePHP.
Em seu terminal execute o seguinte comando:

```sh
bin/cake bake component UserGeneratePass
```
A saída no terminal será algo como:

```sh
Creating file /var/www/cakephp.dev/src/Controller/Component/TestComponentTest.php
Wrote `/var/www/cakephp.dev/src/Controller/Component/TestComponentTest.php`

Creating file /var/www/cakephp.dev/tests/TestCase/Controller/Component/TestComponentTest.php
Wrote `/var/www/cakephp.dev/tests/TestCase/Controller/Component/TestComponentTest.php`

```
Note que nosso Bake já gera um arquivo de test, no para este tutorial não o utilizaremos este arquivo, pode inclusive ficar uma pendência para um proximo post.

Enfim, Nosso component foi criado, agora vamos criar o método responsãvel pela criação de senha:

```php
<?php
namespace App\Controller\Component;

use Cake\Controller\Component;
use Cake\Controller\ComponentRegistry;

class UserGeneratePassComponent extends Component
{
    protected $_defaultConfig = [];

    public function generatePass($length = 10, $uppercase = true, $number = true, $symbol = false)
    {
        $lmin           = 'abcdefghijklmnopqrstuvwxyz';
        $lmai           = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
        $num            = '1234567890';
        $simb           = '!@#$%*-';
        $return         = '';
        $caracters      = '';
        $caracters      .= $lmin;

        if ($uppercase) $caracters .= $lmai;
        if ($number) $caracters .= $num;
        if ($symbol) $caracters .= $simb;

        $len = strlen($caracters);

        for ($n = 1; $n <= $length; $n++) {
             $rand = mt_rand(1, $len);
             $return .= $caracters[$rand-1];
        }

        return $return;
    }
}
```


## Exemplo de uso
No seu controller ```php UserController.php``` por exemplo, você pode chamar o Component da seguinte forma:

```php
<?php

class UserController extends Controller
{
	public function initialize()
    {
        parent::initialize();
        $this->loadComponent('UserGeneratePass');
    }

    public function add()
    {
        $user = $this->Users->newEntity();
        if ($this->request->is('post')) {

            // Gera uma senha com 15 carecteres de números, letras e símbolos
            if (!$user['password']){
                $user['password'] = $this->UserGeneratePass->generatePass(15, true, true, true);
            }

            $user = $this->Users->patchEntity($user, $this->request->data);
            if ($this->Users->save($user)) {
                $this->Flash->success('Usuário adicionado com sucesso.', ['class' => 'alert alert-info']);
                return $this->redirect(['action' => 'index']);
            }
            $this->Flash->error(__('Não foi possível adicionar este usuário, por favor tente novamente.'));
        }

        $this->set('user', $user);
    }
}
```

## Conclusão

Esperemos que este tutorial simples ajude você com o seu desenvolvimento, essa é uma dica bem básica mas que pode salvar vidas (risos).

Se você tiver dúvidas ou encontrar nossos erros no tutorial acima, deixe um comentário abaixo para nos informar.

Caso tenha ficado alguma dúvida, ou tenha outra solução, fique a vontade para deixar seu comentário, ou criar um PR com seu artigo, tenho certeza que a comunidade agradece.
