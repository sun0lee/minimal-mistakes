---
title: "문서화 요건"
excerpt: "문서화."
toc: false
---

<ul>
{% for document in site.kics %}
  {% if document.categories contains 'doc' %}
    <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
    <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul>
