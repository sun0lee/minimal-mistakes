---
title: "생명 장기손해보험위험액"
excerpt: "."
toc: false
categories:
  - scr
tags:
  - scr
---

<ul>
{% for document in site.kics %}
  {% if document.categories contains 'life' %}
    <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
    <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul>
