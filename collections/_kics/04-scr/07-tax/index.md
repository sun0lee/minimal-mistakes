---
title: "IV.7. 요구자본에 대한 법인세효과"
excerpt: "."
toc: false
---

<ul>
{% for document in site.kics %}
  {% if document.categories contains 'tax' %}
    <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
    <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul>
