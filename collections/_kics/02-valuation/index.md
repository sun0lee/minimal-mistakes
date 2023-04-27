---
title: "자산 및 부채 평가"
excerpt: ""
toc: false
categories:
  - kics
tags:
  - kics
---

<ul>
{% for document in site.kics %}
  {% if document.categories contains 'valuation' %}
    <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
    <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul>



<!--ul>
{% for document in site.kics %}
  {% if document.categories contains 'valuation' %}
      <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
      <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul-->
