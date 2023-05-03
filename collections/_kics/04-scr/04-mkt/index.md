---
title: "IV.4. 시장위험액"
excerpt: "."
toc: false
---

<ul>
{% for member in site.data.kicsMeta %}
 {% if member.parentId == '144' %}

  {% capture var01 %}
       {{ member.desc }}
  {% endcapture %}

  {% capture var02 %}
    ## {{ member.id }}. {{ member.title }}
  {% endcapture %}

  <h2><a href="https://sun0lee.github.io/{{ member.path }}">{{ member.title }}</a></h2>
  <p>{{ var01 }}</p>

 {% endif %}
{% endfor %}
</ul>
