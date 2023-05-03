---
title: "blog 시작하기"
excerpt: ""
toc: false
---



<ul>
{% for document in site.blog %}
  {% if document.categories contains 'blog' %}
    <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
    <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul>



**********
### jekyll desc
- [데이터파일 활용 예](https://jekyllrb-ko.github.io/docs/datafiles/)
