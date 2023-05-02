---
title: "IV. 지급여력기준금액 산출"
excerpt: "."
toc: false
categories:
  - kics
tags:
  - kics
---

<ul>
{% for document in site.kics %}
  {% if document.categories contains 'scr' %}
    <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
    <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul>






aaa




<ul>
{% for member in site.data.kicsMap %}
  <li>
    <a href="https://github.com/{{ member.hhh }}">
      {{ member.hhh }}  ,  {{ member.related_ids }}
    </a>
  </li>
{% endfor %}
</ul>
