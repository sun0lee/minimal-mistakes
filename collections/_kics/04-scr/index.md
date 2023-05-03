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








***********



<ul>
{% for member in site.data.kicsHier %}
 {% if member.parent_id == '12' %}

  {% capture var01 %}
       {{ member.desc }}
  {% endcapture %}

  {% capture var02 %}
    ## {{ member.id }}. {{ member.title }}
  {% endcapture %}


   <h3>{{ member.id }}. {{ member.title }} </h3>

   <a href="https://sun0lee.github.io/{{ member.path }}">
         {{ member.title }}
       </a>

  <!--p>{{ var02 | markdownify}}</p-->

  <p>{{ var01 }}</p>
 {% endif %}
{% endfor %}
 </ul>
