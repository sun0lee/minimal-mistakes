---
title: "구성요소"
toc: ture
toc_sticky: true
toc_label: 폴더구조
---
<img src="https://user-images.githubusercontent.com/67420397/233951436-3511f3b9-24ce-4faf-8f85-0a54c9c65020.png" style="width:250px;height:400px;">

## _layout
웹사이트는 보통 하나 이상의 페이지를 가지고 있음. 페이지마다 일일히 템플릿을 구성하는 것은 반복적이고 불필요한 일. 수정도 매우 번거로움
 `_layouts` 이라는 디렉토리에 템플릿을 만들어서 공통적으로 적용함.
jekyll은 HTML 과 markdown을 지원함.
내가 만드는 페이지에서 단 하나만 선언이 가능하며, 내가 만드는 페이지의 모든 내용을 선언 한 Layout의  영역에 출력하는 형태로 미리 만들어 놓은 여러 형태에 맞춰 컨텐츠를 출력하는 방식입니다. 현재의 Layout은 상위 Layout을 지정할 수 있고, 그 상위 Layout은 또 자신의 상위 Layout을 지정하는 형태로 확장이 가능합니다.

## _include (조각파일)
- 네비게이션은 모든 페이지에 있어야 하니까 레이아웃에 추가하는게 바람직함.
- `include` 태그를 사용하면 `_includ` 폴더에 저장된 조각파일의 내용을 참고할 수 있어. 반복되는 소스 코드는 여기에서 관리함.
-  현재 만드는 페이지의 컨텐츠 중 일부 내용을 원하는 형태로 출력하기 위한 페이지 조각의 개념으로 사용하고 있습니다. 때문에 일반적으로 include해서 사용하는 페이지는 파라미터를 통해 데이터를 전달하고 출력을 하도록 합니다.

### 네비게이션
`_includes/navigation.html` 여기에 아래와 같은 navigation.html 파일을 추가해.
```HTML
<nav>
  <a href="/">Home</a>
  <a href="/about.html">About</a>
</nav>
```
## _data
`_data`jekyll은 ymal, json, csv파일로부터 데이터를 읽는 기능을 제공함. 데이터 파일은 소스코드로부터 컨텐츠를 분리하는 좋은 방법.
데이터파일에 네비게이션 컨텐츠를 저장하기  
ymal에 작성한 네비게이션은 html의 네비게이션 코드와 완전 호환됨 : 이걸 지킬이 해줌

## _assets
css, js, images

## _blogging
`_posts` 폴더에 게시물들이 있음  
