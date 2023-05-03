---
title: "III. 지급여력금액 산출"
toc: false
---

<ul>
{% for document in site.kics %}
  {% if document.categories contains 'ac' %}
    <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
    <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul>
