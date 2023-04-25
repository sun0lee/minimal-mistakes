---
title: "Jekyll 설치 및 실행"
toc: ture
toc_sticky: true
toc_label: "Jekyll basic"
---

### Gemfile
jekyll 의존요소를 추가 (화면 로딩에 필요한 버전별 프로그램을 자동으로 정리해줌)
`bundle init` : Gemfile을 생성해줌

### Liquid
템플릿 언어 (object, tag, filter)
- object : 컨텐츠를 어디에 출력할지 liquid에 알려줌  `ruby {{ page.title }}`
- tag :  템플릿의 논리연산과 흐름을 제어함.  
- filter : `|` 로 구분해서 오브젝트의 출력을 변화시킴


<div class="notice--info" markdown="1">
#### Liquid
문법을 알아야 함

```ruby
<html>
  <body>Some body.<body>
</html>
```
</div>

### bundle

- 초안(_drafts) 같이 보기
```bash
bundle exec jekyll serve --port 4000 --trace --drafts  
```

- 일반 실행
```bash
bundle exec jekyll serve --port 4000 --trace
```

- webrick 을 로드하지 못하는 오류가 발생할 때.
```bash
bundle add webrick
```
