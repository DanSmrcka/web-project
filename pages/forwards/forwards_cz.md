---
layout: page
title: Forwards
permalink: /forwards/
ref: forwards
excerpt: ukazka
lang: cz 
nav_order: 3
show_in_nav: true
---


<ul>
{% for forward in site.forwards %}
  <li>
    <a href="{{ forward.url }}">
      {{ forward.title }} - {{ forward.excerpt }}
      <i>{{ site.url }}{{ forward.url }}  </i>
    </a>
  
  </li>
{% endfor %}
</ul>
