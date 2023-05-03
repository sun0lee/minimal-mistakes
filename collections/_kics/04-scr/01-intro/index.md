---
title: "IV.1. 총 칙"
excerpt: ""
toc: false
---

<ul>
{% for member in site.data.kicsMeta %}
 {% if member.parentId == '141' %}

  {% capture var01 %}
       {{ member.desc }}
  {% endcapture %}

  {% capture var02 %}
    ## {{ member.id }}. {{ member.title }}
  {% endcapture %}

  <h2><a href="{{ member.path | relative_url }}">{{ member.title }}</a></h2>
  <p>{{ var01 }}</p>

 {% endif %}
{% endfor %}
</ul>
