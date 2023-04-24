---
title: "about Jekyll"
categories:
  - Test
tags:
  - jekyll
  - tutorials
toc: ture
toc_sticky: true
---


## Gemfile
jekyll 의존요소를 추가 (화면 로딩에 필요한 버전별 프로그램을 자동으로 정리해줌)
`bundle init` : Gemfile을 생성해줌

## Liquid
템플릿 언어 (object, tag, filter)
- object : 컨텐츠를 어디에 출력할지 liquid에 알려줌  `ruby {{ page.title }}`
- tag :  템플릿의 논리연산과 흐름을 제어함.  
- filter : `|` 로 구분해서 오브젝트의 출력을 변화시킴

## front matter (머릿말)

- 머릿말의 title에 제목을 쓰면 각 포스팅의 제목에 나타남
- 머릿말은 `---` 와 `---` 사이에 쓰는 내용임
{: .notice--warning}

## layout
웹사이트는 보통 하나 이상의 페이지를 가지고 있음. 페이지마다 일일히 템플릿을 구성하는 것은 반복적이고 불필요한 일. 수정도 매우 번거로움
 `_layouts` 이라는 디렉토리에 템플릿을 만들어서 공통적으로 적용함.
jekyll은 HTML 과 markdown을 지원함.

## include (조각파일)
네비게이션은 모든 페이지에 있어야 하니까 레이아웃에 추가하는게 바람직해.
`include` 태그를 사용하면 `_includ` 폴더에 저장된 조각파일의 내용을 참고할 수 있어. 반복되는 소스 코드는 여기에서 관리하지  

### 네비게이션
`_includes/navigation.html` 여기에 아래와 같은 navigation.html 파일을 추가해.
```HTML
<nav>
  <a href="/">Home</a>
  <a href="/about.html">About</a>
</nav>
```
## data
`_data`jekyll은 ymal, json, csv파일로부터 데이터를 읽는 기능을 제공함. 데이터 파일은 소스코드로부터 컨텐츠를 분리하는 좋은 방법.
데이터파일에 네비게이션 컨텐츠를 저장하기  
ymal에 작성한 네비게이션은 html의 네비게이션 코드와 완전 호환됨 : 이걸 지킬이 해줌

## assets
css, js, images

## blogging
`_posts` 폴더에 게시물들이 있음  
