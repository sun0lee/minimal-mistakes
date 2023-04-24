---
title: "레이아웃"
toc: ture
toc_sticky: true
toc_label: 다루는 내용
---

### Front Matter, YAML
- **YAML**은 "YAML Ain't Markup Language"의 약자로, 마크업 언어가 아닌 데이터 직렬화 언어입니다. 즉, 데이터를 사람이 쉽게 읽고 쓸 수 있는 텍스트 형식으로 표현하는 언어입니다. YAML은 XML, JSON 등과 함께 대표적인 데이터 직렬화 언어 중 하나입니다. YAML은 빈 공간으로 이루어진 계층 구조로 표현되며, 들여쓰기를 통해 하위 요소와 상위 요소를 구분합니다. YAML은 주로 설정 파일, 데이터 저장 및 전송, 템플릿, 로그 파일 등에서 사용됩니다.
- **Front Matter**는 사용자가 생성하는 HTML, 마크다운 형식의 페이지 또는 포스트 문서내에서 `---` 으로 시작하고, 끝나는 블럭 사이에 사용하는 YAML 형식을 의미합니다.
- 적용 우선순위 : Front Matter(`---`) > `_layout` > `_config.yml`

### tmi

{% capture notice-2 %}
#### 직렬화언어
- serialization : 객체의 상태나 데이터를 저장하거나 전송하기 위해 일련의 바이트로 변환하는 과정
- 이때 사용되는 언어를 직렬화 언어(serialization language)
- 대표적인 직렬화 언어로는 XML, JSON, YAML
{% endcapture %}

<div class="notice">
  {{ notice-2 | markdownify }}
</div>

## front matter (머릿말)

- 머릿말의 title에 제목을 쓰면 각 포스팅의 제목에 나타남
- 머릿말은 `---` 와 `---` 사이에 쓰는 내용임
{: .notice--warning}

## _layout
- 웹사이트는 보통 하나 이상의 페이지를 가지고 있음. 페이지마다 일일히 템플릿을 구성하는 것은 반복적이고 불필요한 일. 수정도 매우 번거로움
- `_layouts` 이라는 디렉토리에 템플릿을 만들어서 공통적으로 적용함.
- jekyll은 HTML 과 markdown을 지원함.
