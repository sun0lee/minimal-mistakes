---
title: "intro"
permalink: /kics-index/
toc: false
---

> - 지급여력이란 지급능력(solvency), 즉 보험계약자에 대한 보험금지급 의무의 이행을 위해 필요한 자산(책임준비금) 외에 추가로 보유하도록 한 순자산을 의미함. **<u>지급여력금액</u>** 이란 보험회사가 예측할 수 없는 리스크의 발생에 대비할 수 있는 일종의 충격흡수장치(buffer) 또는 잉여금 (surplus)이라고 할 수 있음. K-ICS는 이 지급여력금액 (순자산 금액)을 측정하기 위해, 장부금액을 사용하지 않고, 자산과 부채를 시가평가 기준으로 재평가하여 산출함.
>
> - **<u>지급여력기준금액</u>** 은 시장리스크, 보험리스크, 신용리스크, 운영리스크 등의 각 리스크측면에서 자산 및 부채에 잠재적인 경제적 손실이 발생할 위험(향후 1년간 99.5% 신뢰수준 내에서 각 관련 요인 변동으로 인해 발생 가능한 손실)을 합리적으로 산출한 금액을 의미함.
>
> - **<u>지급여력비율</u>** 은 지급여력금액을 지급여력기준금액으로 나눈 비율로서, 향후 1년 동안 발생가능한 위험액에 대비하여 얼마만큼의 버퍼를 갖추고 있는지 수준을 의미함. 이는 보험회사의 재무건전성을 측정하는 핵심지표로 활용됨.

시가평가를 기반으로 하는 보험부채 평가 기준인 IFRS 17 시행에 따라 지급여력제도의 정합성을 제고하기 위해 보험부채 시가평가를 기반으로 하는 새로운 지급여력제도(K-ICS) 도입을 추진함. 신지급여력제도 (K-ICS)는 요구자본 측정 신뢰수준을 현 99%에서 99.5%로 상향하고, 기존 위험계수방식에서 벗어나 시나리오 방식을 적용함으로 경제환경에 따른 자본변동성 등 리스크를 보다 정밀하게 측정함.

<!--
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
</ul-->

<!-- 페이지의 excerpt(요약 발췌)  https://pengpengto.gitlab.io/blog/tech/2017/06/29/jekyll-excerpt_option.html -->
<ul>
  {% for document in site.kics %}
    {% if document.title != "intro" and document.categories contains 'kics' %}
      <li><a href="{{ document.url }}">{{ document.title }}</a></li>
      <!--p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p-->
    {% endif %}
  {% endfor %}
</ul>
