---
#layout: collection
title: "intro"
collection: kics
permalink: /kics-index/
author_profile: false
# toc: true
# toc_sticky: true
---

시가평가를 기반으로 하는 보험부채 평가 기준인 IFRS 17 시행에 따라 지급여력제도의 정합성을 제고하기 위해 보험부채 시가평가를 기반으로 하는 새로운 지급여력제도(K-ICS) 도입을 추진함.
신지급여력제도 (K-ICS)는 요구자본 측정 신뢰수준을 현 99%에서 99.5%로 상향하고, 기존 위험계수방식에서 벗어나 시나리오 방식을 적용함으로 경제환경에 따른 자본변동성 등 리스크를 보다 정밀하게 측정함.


<!--ul>
  {% for document in site.kics %}
    {% if  document.title != "intro" and document.path contains "/index.md" %}
      <li>
        <a href="{{ document.url }}">{{ document.title }}</a>
        {{ document.excerpt | strip_html | truncatewords: 45, '...' }}
      </li>
    {% endif %}
  {% endfor %}
</ul-->

{% assign sorted_docs = site.kics | sort: 'title' %}
<ul>
  {% for document in sorted_docs %}
    {% if document.title != "intro" and document.path contains "/index.md" %}
      <li>
        <a href="{{ document.url }}">{{ document.title }}</a>
        {{ document.excerpt | strip_html | truncatewords: 45, '...' }}
      </li>
    {% endif %}
  {% endfor %}
</ul>

<!-- 페이지의 excerpt(요약 발췌)  https://pengpengto.gitlab.io/blog/tech/2017/06/29/jekyll-excerpt_option.html -->
