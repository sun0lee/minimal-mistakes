---
title: "지급여력기준금액 산출"
excerpt: "."
toc: false
---

<ul>
{% for document in site.kics %}
  {% if document.categories contains 'scr' %}
    <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
    <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul>
