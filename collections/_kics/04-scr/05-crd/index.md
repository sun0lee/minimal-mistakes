---
title: "신용위험액"
excerpt: "."
toc: false
categories:
  - scr
tags:
  - scr
---

<ul>
{% for document in site.kics %}
  {% if document.categories contains 'crd' %}
    <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
    <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul>
