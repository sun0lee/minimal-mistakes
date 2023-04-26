---
title: "구성요소"
categories:
  - jekyll
tags:
  - layout
  - include
  - data
  - assets
  - site
toc: ture
toc_sticky: true
toc_label: 폴더구조
---


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


## _site

`_site` 디렉토리는 빌드된 HTML 및 기타 파일(css, js, 이미지 등)들이 저장되는 디렉토리이다. 당연히 이 디렉토리 안의 파일들은 빌드되지 않는다.

만약 `_site` 말고 다른 디렉토리를 사용하고 싶다면 `_config.yml`에서 destination 설정에 값을 입력하면 된다(디폴트: `./_site`).

`bundle exec jekyll serve` 명령어로 테스트 서버를 새로 열 때마다 `_site` 디렉토리 안의 모든 내용은 삭제되고 새로 빌드된 파일들이 저장된다. 만약 이 디렉토리 안에 반드시 남겨야 하는 디렉토리 혹은 파일이 있다면 `_config.yml`에서 keep_files 설정에 추가하면 된다.[^1]

[^1]: `_site` 디렉토리로부터 시작하는 상대 경로로 입력하면 된다. ex. `keep_files: ["home.html", "debug/"]`

[이전 글]에서 설명했듯이, 깃허브 페이지에서는 허용된 플러그인 이외의 사용이 금지되어 있다. 만약 반드시 플러그인을 사용해야 한다면 로컬에서 빌드한 후 빌드된 파일을 깃허브 저장소(Repository)에 push하면 되는데, 바로 `_site` 디렉토리를 그대로 push하면 된다.

만약 플러그인을 사용하지 않고 지킬 디렉토리 그 자체로 그대로 올린다면 `_site` 디렉토리는 굳이 없어도 된다. 어차피 깃허브 페이지가 자체적으로 빌드를 다시 하기 때문이다. 따라서 `.gitignore`에 `_site`를 추가하는 것이 좋다.
