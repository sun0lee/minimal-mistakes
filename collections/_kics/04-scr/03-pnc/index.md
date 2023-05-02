---
title: "IV.3. 일반손해보험위험액"
excerpt: "."
toc: false
categories:
  - scr
tags:
  - scr
---

<ul>
{% for document in site.kics %}
  {% if document.categories contains 'pnc' %}
    <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
    <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul>

보유리스크율_(비례-연동)

- 수식으로 입력 : ${보유리스크율_{(비례-연동)}}$ 은 보장단위별로 재보험수수료가 손해율에 연동되는 비례 재보험을 체결한 후에 예상되는 손실액

- `<sub>` tag로 입력 : 보유리스크율<sub>(비례-연동)</sub> 은 보장단위별로 재보험수수료가 손해율에 연동되는 비례 재보험을 체결한 후에 예상되는 손실액
