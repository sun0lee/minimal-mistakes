---
title: "IV.6. 운영위험액"
# excerpt: "."
---

<!--ul>
{% for document in site.kics %}
  {% if document.categories contains 'oper' %}
    <h2><a href="{{ document.url }}">{{ document.title }}</a></h2>
    <p>{{ document.excerpt | strip_html | truncatewords: 45, '...' }}</p>
  {% endif %}
{% endfor %}
</ul-->

# 6-1. 익스포져 산출기준

## 가. 측정대상
운영위험액은 보험회사의 모든 원수 및 수재보험계약, 역외출재보험계약을 대상으로 측정한다.
- (1) 변액보험, 퇴직보험 및 퇴직연금 등도 운영위험이 존재하므로 측정대상에 포함한다.

## 나. 익스포져
익스포져는 일반운영위험 익스포져와 기초가정위험 익스포져로 구분한다.

<div class="mermaid">
flowchart TD
    A[운영리스크 익스포져] --> B(일반운영위험 익스포져)
    A --> C(기초가정위험 익스포져:원수)
    B --> B1(보험료익스포져)
    B1 --> B3(직전1년 초과납입보험료)
    B1 --> B4(역외출재경과보험료)
    B --> B2(현행추정부채 익스포져)
    C --> C1(지급금예실차 익스포져)
    C --> C2(사업비예실차 익스포져)

</div>

### (1) 일반운영위험 익스포져
일반운영위험 익스포져는 보험료 익스포져와 현행추정부채 익스포져로 구분한다.
#### 1.보험료 익스포져
보험료 익스포져는 직전 1년간 납입된 보험료 및 직전 1년간 초과 납입된 보험료로 한다. 다만, 일반손해보험의 경우는 역외출재계약 경과보험료를 포함한다.
##### ᄀ. 직전 1년간 초과 납입된 보험료
생명·장기손해보험 및 일반손해보험의 직전 1년간 초과 납입된 보험료는 직전 1년 납입된 보험료가 직직전 1년 납입된 보험료의 120%를 초과하는 경우 초과된 금액으로 산출한다.

<details>
  <summary>초과 납입된 보험료에 대해 별도의 위험계수를 부과하는 이유</summary>
  <div markdown="1">
  {% capture notice-1 %}
- 운영리스크는 ‘부적절하거나 잘못된 내부의 절차, 인력 및 시스템 또는 외부의 사건으로 인해 발생하는 손실위험’으로 정의하고, 수입보험료 및 현행추정부채를 익스포져로 하는 위험계수 방식으로 산출
- 보험회사가 급격하게 성장하거나, 공격적으로 영업을 할 경우, 운영리스크가 추가로 발생할 가능성이 크므로 이를 반영하기 위해 수입보험료 성장금액(초과 납입된 보험료)을 별도의 익스포져로 사용하되,
  - 전년 대비 성장 폭이 큰 경우에만 리스크로 측정하기 위해 직전 1년 납입된 보험료가 직직전 1년 납입된 보험료의 120%를 초과하는 경우 그 초과된 금액을 익스포져로 사용
  {% endcapture %}
  <div class="notice">
    {{ notice-1 | markdownify }}
  </div>
  </div>
</details>

##### ᄂ. 역외출재계약의 출재경과보험료
역외출재계약의 경과보험료는 결산시점에 보유하고 있는 역외출재계약의 출재경과보험료를 말한다.

<details>
  <summary>역외출재계약을 운영위험액으로 산출하는 이유</summary>
  <div markdown="1">
  {% capture notice-1 %}
- 역외 재보험거래의 경우, 거래 특수성(국내 영업소 미설치 등으로 재보험금 정산 절차가 복잡하고 지급 지연 및 거절 사례도 발생)과 고정이하 미수금이 높은 특정을 고려하여 신용 위험을 차등화할 필요가 있으나,
- 신용리스크는 거래상대방 신용등급을 기초로 측정하기 때문에 역내·외 구분에 따라 신용 위험계수를 차등화할 수 없는 측면, 그리고 역외 재보험거래의 복잡성 및 법률문제 등은 운영리스크 특성에 더 부합하는 측면을 고려하여
  - K-ICS는 역외출재계약에 내재된 신용위험을 신용리스크가 아닌 운영리스크에서 측정하며, 역외재보험 경과보험료에 위험계수를 적용하여 산출
  {% endcapture %}

  <div class="notice">
    {{ notice-1 | markdownify }}
  </div>
  </div>
</details>


#### 2.현행추정부채 익스포져
현행추정부채 익스포져는 생명·장기손해보험 및 일반손해보험의 결산시점 현행추정부채로 한다.

### (2) 기초가정위험 익스포져
기초가정위험 익스포져는 생명보험계약 및 장기손해보험계약을 대상으로 측정하며, 지급금 예실차 익스포져와 사업비예실차 익스포져로 구분한다.

{% capture notice-text %}
**기초가정리스크 개요**
- 기초가정을 낙관적으로 사용하면 시간 경과에 따른 예실차<sup>1)</sup> 누적  또는 보험부채 증가로 손실 금액이 확대되므로 기초가정의 낙관적 사용에 따른 손실금액에 대한 요구자본 측정 필요
  - 1)예실차 : 보험부채 평가에 사용한 계리적 가정(예상)과 경험 실적(실제) 간의 차이
- 기초가정위험 관련 요구자본을 측정하지 않을 경우, 낙관적인 가정 사용시 가용자본만 증가하므로 보험회사가 K-ICS비율 제고 목적으로 가정을 낙관적으로 사용할 유인이 발생
- 낙관적 기초가정 사용으로 인한 손실위험을 내부통제 기능 부실로 간주하여 운영리스크 內 기초가정 리스크 신설
{% endcapture %}

<div class="notice">
  {{ notice-text | markdownify }}
</div>

#### 1. 지급금예실차 익스포져
지급금예실차 익스포져는 원수계약을 대상(단, 공동재보험의 경우 수재계약 포함)으로 하며, 보험요소(사망률·위험률 등)로 인한 발생손해액에 대해 다음의 기준에 따라 산출한다.
- ᄀ. 1년 전 시점의 보유계약을 기준으로 1년 간의 실제 지급금에서 1년전 시점의 부채 장래현금 흐름 상 최초 12개월분의 예상 지급금을 차감하여 산출한다. 단, 지급금예실차 익스포져가 음수(-)인 경우 0으로 한다.
- ᄂ. 보험회사가 지급을 예상하지 못하여 기초가정에 포함하지 않은 지급금(판결로 인한 보험금 지급 등)이라 하더라도 “ᄀ.”의 실제 지급금에 포함하여야 한다.
- ᄃ. 납입면제 등을 통해 보험료를 감소시킨 경우, 해당 금액을 “ᄀ.”의 실제 지급금에 포함 하여야 한다.  

<details>
  <summary>지급금예실차 익스포져 대상</summary>
  <div markdown="1">
  {% capture notice-1 %}

**기초가정리스크를 원수계약 대상(공동재보험의 경우 수재계약 포함)으로만 측정하는 이유** :
수재계약은 보험회사의 낙관적인 기초가정 사용과 무관하게 예상치 못한 대규모 사고에 노출 되는 특성, 보험료와 보험금의 변동성이 동시에 발생하는 특성 등을 고려하여 대상에서 제외함. 다만, 공동재보험 수재계약의 경우, 원수계약과 계약 특성이 동일하므로 기초가정리스크 측정대상에 포함
  {: .notice--primary}

**지급금예실차 익스포져 산출 시 보험요소로 인한 발생손해액만 포함하는 이유** :
투자요소는 보험료와 지급금을 종합적으로 고려해야 하며, 회사의 계리적 가정 外 감독기준 (공시이율 등)에 의해서도 예실차가 발생할 수 있으므로 산출대상에서 제외
{: .notice--primary}

**기초가정에 포함하지 않은 지급금을 지급금예실차위험 익스포져의 실제 지급금에 포함하는 이유** :
판결로 인한 보험금 지급 등 보험회사가 예상하지 못한 지급금은 기초가정에는 포함하지 않을 수 있으나, 회사가 통제할 수 없는 손실위험에 해당하므로 모두 포함할 필요
{: .notice--primary}

**보험료를 감소시킨 경우 해당 금액을 지급금예실차위험 익스포져의 실제 지급금에 포함하는 이유** :
보험회사가 기초가정리스크 축소를 위해 보험금을 지급하는 대신 보험료를 감액하는 방식을 선택할 수 있으므로 보험료를 감소시킨 경우 해당 금액을 실제 지급금에 포함
{: .notice--primary}
  {% endcapture %}

  <div class="notice">
    {{ notice-1 | markdownify }}
  </div>
  </div>
</details>

#### 2. 사업비예실차 익스포져
사업비예실차 익스포져는 원수계약을 대상(단, 공동재보험의 경우 수재계약 포함)으로 하며, 다음의 기준에 따라 산출한다.
- ᄀ.1년 전 시점의 보유계약을 기준으로 1년 간의 실제 사업비에서 1년전 시점의 부채 장래 현금흐름 상 최초 12개월분의 예상 사업비를 차감하여 산출한다. 단, 사업비예실차 익스 포져가 음수(-)인 경우 0으로 한다.
- ᄂ. 보험계약 의무이행과 관련되지 않은 일회성 비용으로서 기초가정에서 제외한 사업비(명예 퇴직금 등)의 경우, “ᄀ.”의 실제 사업비에서 제외한다.

**기초가정에서 제외한 사업비를 사업비예실차위험 익스포져의 실제 사업비에서 제외하는 이유** :
사업비는 지급금과 달리 보험회사가 통제할 수 있는 부분이므로 기초가정에서 제외한 사업비의 경우 익스포져 산출 시 실제 사업비에서도 제외
{: .notice}


# 6-2. 운영위험액 산출기준
## 가. 운영위험액
운영위험액은 각각의 측정대상 익스포져에 해당 위험계수를 곱하여 산출한 후 합산한다.

## 나. 일반운영위험액
일반운영위험액은 생명·장기손해보험의 변액보험, 퇴직보험 및 퇴직연금, 이외 생명· 장기손해보험, 일반손해보험으로 상품군을 구분하여 일반운영위험액을 각각 계산한 후 이를 합산하여 보험회사의 전체 일반운영위험액을 산출한다.
### (1) 산출방법
“나.”의 각 상품군은 주계약(기본계약) 기준으로 분류하며, 각 상품군별 일반운영위험액은 보험료 익스포져에 해당 위험계수를 곱하여 산출된 일반운영위험액과 현행추정부채 익스포져에 해당 위험계수를 곱하여 산출된 일반운영위험액 중 큰 금액으로 한다.
### (2)위험계수
 일반운영위험액의 보험료 익스포져 및 현행추정부채 익스포져에 적용하는 위험계수는 <표40>과 같다.

 ![image](https://user-images.githubusercontent.com/67420397/235455907-af3b6ba1-0310-4590-84b7-de079a395027.png)

 <details>
   <summary>일반운영위험액 위험계수 도출 근거</summary>
   <div markdown="1">
   {% capture notice-1 %}
- 생명·장기손보와 일반손보로 구분하여 보험료 및 부채 부문의 운영리스크를 산출하며, 각 부문별 위험계수의 수준은 ICS의 위험계수를 준용한다. 다만 국내의 경우 계약 유지율이 낮아 신계약 보험료 영향이 과도한 측면이 있어, ICS 위험계수 대비 보험료 부문은 낮추고, 부채 부문은 높여 보험료·부채 부문의 운영리스크 균형을 도모
- 또한 생명·장기 부문의 경우 변액 및 퇴직연금 상품은 일반적인 생명·장기 상품과 영업, 계약관리 및 자산운용 방식에 있어 차이가 있으므로, 변액 및 퇴직연금 상품은 독립된 단위로 운영위험액을 측정
- 역외출재 경과보험료 위험계수는 국내 보험회사 통계를 활용하여 아래와 같이 산출
  - 위험계수 = 경과보험료당 손해율 $$\cdot$$ 역내외출재손해액 미수금 회수율 차이

   {% endcapture %}

   <div class="notice">
     {{ notice-1 | markdownify }}
   </div>
   </div>
 </details>

## 다. 기초가정위험액
기초가정위험액은 지급금예실차위험액과 사업비예실차위험액을 합산하여 산출한다.

**지급금예실차위험액과 사업비예실차위험액을 단순 합산하는 이유** :
기초가정위험액은 낙관적 기초가정을 사용한 보험회사에 대해 산출되므로 세부 위험이 동시에 발생하는 것으로 가정하는 방식이 합리적 (☞상관관계=1)
{: .notice}

### (1) 지급금예실차위험액
지급금예실차위험액은 다음의 기준에 따라 산출한 _한도금액을 초과한 익스포져_ 에 위험계수를 곱하여 산출한다.
1. 한도금액은 1년 전 시점의 보유계약을 기준으로 1년 간의 예상 지급금에 5%를 곱한 금액으로 한다.
2. 익스포져는 [**6-1.나.(2).1. 지급금예실차 익스포져**](#1-지급금예실차-익스포져)에 따라 산출한 금액으로 한다.
3. 위험계수는 3.5를 적용한다.

**_한도금액을 초과한 익스포져에 대해서만 지급금예실차위험액을 산출_ 하는 이유** :
회사가 기초가정을 적정하게 관리하더라도 예상치 못한 대규모 보험금 지급 등으로 지급금 예실차가 크게 발생할 수 있으므로 일정 한도(1년 전 보유계약 기준 직전 1년 예상 지급금 5%) 이내의 단기 변동성에 대해서는 리스크를 미측정. 반면, 사업비예실차위험액의 경우 지급금예실차위험액과 달리 보험회사가 통제할 수 있는 부분이므로 위험액 산출 시 한도 미부과
{: .notice}

### (2) 사업비예실차위험액
사업비예실차위험액은 다음의 기준에 따라 산출한 익스포져에 위험계수를 곱하여 산출한다.
1. 익스포져는 [**6-1.나.(2).2. 사업비예실차 익스포져**](#2-사업비예실차-익스포져)에 따라 산출한 금액으로 한다.
2. 위험계수는 3.7을 적용한다.