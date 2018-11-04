---
layout: page
title: Autores
permalink: /autores/
description: "Página de Autores"
header-img: "assets/img/post-bg-04.jpg"
---

# Autores

{% for page in site.pages %}
    {% if page.author != null %}
<p>
    <a href="{{ page.url | prepend: site.baseurl }}">{{ page.author }}</a>
</p>
    {% endif %}
{% endfor %}