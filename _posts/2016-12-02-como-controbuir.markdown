---
layout: post
title:  "Como contribuir!"
date:   2016-12-02 12:40:06 -0200
categories: avisos
author: 'Erik Figueiredo'
author_url: 'http://www.webdevbr.com.br'
author_url_label: 'WebDevBr'
comments: true
---
Bem vindos ao novo Blog do CakePHP Brasil, infelizmente o projeto com Wordpress não é muito simples de manter pelo motivo de ser mais um dashboard para acompanhar, algumas pessoas acabaram ficando chateadas comigo, então, em uma tentativa de ressucitar o blog, montei usando Jekyll, Jenkins e GitHub, assim a coisa fica mais automatizada e o gerenciamento se da através do GitHub, aonde eu já estou logado o dia todo.

Uma vantagem desta nova abordagem é forçar a comunidade a interagir mais com o GitHub e quem sabe contruir seu portfólio por lá.

Para saber o que tem pra fazer em cada repostório do GitHub do CakePHP Brasil, entre nas issues de cada projeto, por exemplo, você quer ver o que pode ser melhorado neste projeto, visite nossa organização no link [github.com/CakePHPBrasil](https://github.com/CakePHPBrasil), escolha o repositório **blog** na lista e depois clique em **issues** no topo, por exemplo, caso você queira ver as ideias de artigos enviadas pela comunidade, [clique aqui](https://github.com/CakePHPBrasil/blog/issues?q=is%3Aopen+is%3Aissue+label%3Aarticle).

## Quero enviar um artigo

Para enviar novos artigos é muito simples, dentro do diretório `_posts` adicione um arquivo seguindo a seguinte convenção `YYYY-MM-DD-nome-do-post.markdown` em seguida adicione o seu texto usando o formato markdown (é bem simples, não se assuste).

No topo do arquivo você configura conforme a seguir:

{% highlight plan %}

---
layout: post
title:  "Como contribuir!"
date:   2016-12-02 12:40:06 -0200
categories: avisos
author: 'Erik Figueiredo'
author_url: 'http://www.webdevbr.com.br'
author_url_label: 'WebDevBr'
comments: true
---

{% endhighlight %}

 * **layouts**: define o layout desta página, não altere
 * **title**: Título do artigo
 * **date**: Data da pubicação no formato YYYY-MM-DD HH:MM:SS, o -0200 é o timezone
 * **categories**: Categorias que este artigo pertence, caprixe nisso
 * **author**: Seu nome
 * **author_url**: Um link que você queira postar, para que as pessoas te encontrem, seu portifólio, enfim...
 * **author_ur_label**: O texto ancora para seu link
 * **comments**: habilita e desabilita comentários

O Jekyll que faz o build para o HTML fornece alguns recursos legais, como este **code highlight** a seguir:

{% highlight php %}
<?php

namespace App\Controller;

class UsersController extends AppController
{
    public function login()
    {
        /**...**/
    }
}

{% endhighlight %}

Assim que receber seu pull request vamos analizar e aceitar ou indicar correções, se necessário.

Precisa de ideias para artigos ou quer ajudar alguém, [clique aqui](https://github.com/CakePHPBrasil/blog/issues?q=is%3Aopen+is%3Aissue+label%3Aarticle).

Qualquer coisa fico a disposição de vocês!

Obs.: Não esqueçam de adicionar seu nome e um link no fim do artigo para que quem ler e quiser algum serviço ou trocar uma ideia com vocês, possam encontrá-los.

