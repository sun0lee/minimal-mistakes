---
title: "markdown + html tag + template "
categories:
  - blog
tags:
  - blog, markdown
---

# 0. 들어가며.
블로그의 글은 확장자가 .md (markdown)인 마크다운 형식으로 작성함.   
collections 내에 주제별 폴더가 있고, 글을 작성하려는 폴더 내에 .md 파일을 추가하면 블로그에 글이 추가됨.

마크다운은 쉽게 말해 문서를 작성할 때 **굵게** , _기울임_ , <u>밑줄(이건 마크다운은 아니고 html 태그임)</u> 이런 식으로 문서를 보기쉽게 근데 쓰기도 쉽게 쓰는것을 추구하면서 만들어진 것이라고 함.

아래에는 마크다운의 기본문법들을 설명함. 아래 내용은 출처에서 참고하여 작성함!! 마크다운은 설명을 읽는 것보다 직접 따라서 써보면 금세 익히므로 아래 참고하기.

추가로 더 디테일하게 뭔가 조잡스러운걸 하고 싶다면 html tag를 알아야 함. (아직 나도 잘 모름)

- [본문출처 : https://gist.github.com/ihoneymon/652be052a0727ad59601](https://gist.github.com/ihoneymon/652be052a0727ad59601)


# 1. Header
- **제목수준** : toc(table of contents)에 header의 수준에 따라 자동으로 잡히기 때문에 문서구조 및 하이라키 수준에 맞춰서 사용하기.   
- **적용방법** : '#'의 갯수에 따라 Header 수준이 정해지는데 원하는 수준의 #와 띄어쓰기 한칸이면 적용됨.
- __적용예시__ : 이렇게 작성하면
```markdown
# 1-1. 제일 큰 제목
## 가. 2번째 큰 제목
### (1) 3번째 수준 제목
#### 1. 4번째 제목 기준서에서는 ①로 표기.
##### ㄱ. 5번째 제목
###### 6번째 제목
```
<br>
- __적용예시__ : 이렇게 화면에 보임.
# 1-1. 제일 큰 제목
## 가. 2번째 큰 제목
### (1) 3번째 수준 제목
#### 1. 4번째 제목 기준서에서는 ①로 표기.
##### ㄱ. 5번째 제목
###### 6번째 제목


****


# 2. 인용 (BlockQuote)
- **적용방법** : '>' 와 띄어쓰기 한칸 그 다음 쓰고 싶은 내용을 쓴다.

```markdown
> 이렇게
>	> 쓰면
>	>	> 어떻게 나올까
```

> 이렇게
>	> 쓰면
>	>	> 어떻게 나올까

```markdown
> "이렇게
써도
된다."
```

> "이렇게
써도
된다."

```markdown
> 섞어서 써보기
## 이게 된다고 ?
- 된다.
```

> 섞어서 써보기
## 이게 된다고 ?
- 된다.

****


# 3. 목록

## 3-1. 넘버링
```markdown
1. 1만 써도
1. 순서대로
100. 넘버링이 된다(몇을 쓰든)
```
1. 1만 써도
1. 순서대로
100. 넘버링이 된다(몇을 쓰든)


## 3-2. 순서가 없는 목록

- '-','+'.'*' + 띄어쓰기 한칸이면 목록이 생성된다. 수준 조정은 기호 앞에 띄어쓰기 갯수에 따라 결정된다. 점점 내려감.

```markdown
* 목록
  * 하위 목록
    * 하위하위 목록

- 목록
  - 하위 목록
    - 하위하위 목록

+ 목록
  + 하위 목록
    + 하위하위 목록
```
* 목록
  * 하위 목록
    * 하위하위 목록

- 목록
  - 하위 목록
    - 하위하위 목록

+ 목록
  + 하위 목록
    + 위하위 목록

*****

# 4. code (프로그램 소스 입력할 때)

## 4-1. 블록으로 입력하기
- 입력방법 : '`' 백틱 Backtick 3개를 연달아서 쓰고 + 코드 언어 (java, sql, html 등 )를 쓰면 해당하는 코드기준으로 알록달록 잘보이게 나타난다.
  - 블록으로 코드를 작성하고 다시 '`' 백틱 3개로 문을 닫아준다.
  - 이건 설명을 읽을게 아니라 직접 해보면 아무것도 아님.

```java
// 여기 주석도 가능함. 주석처럼 보임 !!
  public static void main(String[] args) {
    System.out.println("Hello, world");
```

## 4-2. inline code
- 입력방법 : 입력하고 싶은 inline 코드를 '`' 백틱 Backtick 1개로 감싼다.
- 인라인 코드는 이렇게 글 속에  `System.out.println("Hello, Honeymon")` 코드가 들어 있는걸 의미함.
- 이것도 해보면 아무것도 아님.

*****

# 5. 링크

```markdown
사용문법: [Title](link, "마우스를 가져다대면 나오는 설명")
적용예: [_**링크 이름**_ :굵게 그리고 기울여서 ](https://google.com "링크 설명")
```

- [_**링크이름**_ : 굵게 그리고 기울여서 ](https://google.com "링크 설명 ")

*****

# 6. 강조
```markdown
*이것은 기울임*
_이것도 기울임_
**이것은 굵게**
__이것도 굵게__
~~취소선~~
<u> 밑줄 </u>

___기울임 + 굵게___
___~~기울임 + 굵게 + 취소~~___
___<u>기울임 + 굵게 + 밑줄 =  조잡스럽지만 가능</u>___
```

- *이것은 기울임*
- _이것도 기울임_
- **이것은 굵게**
- __이것도 굵게__
- ~~취소선~~
- <u> 밑줄 </u>

- ___기울임 + 굵게___
- ___~~기울임 + 굵게 + 취소~~___
- ___<u>기울임 + 굵게 + 밑줄 = 조잡스럽지만 가능</u>___

> ```문장 중간에 사용할 경우에는 **띄어쓰기** 를 사용하는 것이 좋다고 한다.```   
> 문장 중간에 사용할 경우에는 띄어쓰기를 사용하는 것이 좋다고 한다.


- 위첨자 `<sup> ` tag로 입력 주석 달 때 사용: 보유리스크율<sup>1)</sup>
- 아래첨자 `<sub>` tag로 입력 : 보유리스크율<sub>(비례-연동)</sub>


*****

# 7. 그림 (이미지)
- 이미지 파일은 "경로"에 "실제 파일"이 필요하다.
- [ ] 블로그 폴더구조의 `assets > images` 에 직접 파일을 넣고 관리해도 되고,
- [x] 웹에 upload 한 이미지 파일의 주소만 알아도 된다.

{% capture notice-text %}
**캡쳐한 이미지 파일을 웹에 올리고 주소를 따오는 엄청 쉬운 방법**
1. 필요한 이미지를 캡쳐해서 클립보드에 복사(`ctrl + c`)한다.
2. 깃허브 자기 프로젝트에 issue 에 들어가서 https://github.com/sun0lee/sun0lee.github.io/issues
3. 우측 상단의 초록색 `new issue` 버튼을 클릭
![예제도](https://user-images.githubusercontent.com/67420397/235714881-bc93680c-252c-47b9-b318-5d5fd17fb9d1.png "초간단 사진올리기1")
4. `ctrl + v` 붙여넣기
5. 3초 정도 흐르면 링크가 생성된다.
![설명은 생략가능](https://user-images.githubusercontent.com/67420397/235715325-abcb98a7-5275-4e5c-ba74-80eeda9cdaad.png)
{% endcapture %}
<div class="notice">
  {{ notice-text | markdownify }}
</div>

```markdown
![Alt text](/path/to/img.jpg)
![Alt text](/path/to/img.jpg "사진에 대한 설명은 여기에")
```

*****

# 8. 줄바꿈
- 적용방법 : 3칸 이상 띄어쓰기(` `)를 하면 줄이 바뀐다. 은근이 많이 쓰게 됨. 중요함. 써보면 알게 됨.  

```markdown
* 줄 바꿈을 하기 위해서는 문장 마지막에서 3칸이상을 띄어쓰기해야 한다.
이렇게

* 줄 바꿈을 하기 위해서는 문장 마지막에서 3칸이상을 띄어쓰기해야 한다.___\\ 띄어쓰기
이렇게
```

* 줄 바꿈을 하기 위해서는 문장 마지막에서 3칸이상을 띄어쓰기해야 한다. 이렇게

* 줄 바꿈을 하기 위해서는 문장 마지막에서 3칸이상을 띄어쓰기해야 한다.    \
이렇게

*****

# 9. 표 (table)
~~~markdown
| 헤더0 | 헤더1 | 헤더2 |
|:---:|:---:|:---:|
| a1  | a2  | a3  |
| b1  | b2  | b3  |
~~~

| 헤더0 | 헤더1 | 헤더2 |
|:---:|:---:|:---:|
| a1  | a2  | a3  |
| b1  | b2  | b3  |

- ':'에 따라서 가운데 정렬, 왼쪽정렬 오른쪽 정렬이 된다.
- 표는 솔직히 직접 입력하기 좀 귀찮아서 아래처럼 컨버팅 해주는 웹페이지를 이용한다.
> [엑셀을 붙여넣으면 마크다운 표로 컨버팅해주는 홈페이지 markdown-generator](https://tableconvert.com/ko/markdown-generator)

*****

# 10. notice ()
이건 마크다운에서 지원하는게 아니라 minimal mistake 테마에서 지원하는 기능임. 글을 쓸때 뭔가 강조하고 싶고 네모난 음영안에 넣어두고 싶을때 사용함.

## 10-1. 한단락만 notice
**예를들면**  :     바로 이렇게 `{: .notice--info}`를 단락 아래에 입력하면 해당 단락이 네모난 알림상자? 안에 들어온다. 색깔은 여러가지인데 아래에서 하나씩 설명해보면.    여기에는 띄어쓰기를 세칸 넣어도 단락구분이 안됨 ㅠㅠ..
{: .notice--info}

**primary** : 진한 회색 `{: .notice--primary}`
{: .notice--primary}

**default** : 흐린 회색 `{: .notice}`
{: .notice}

**warning** : 주황 `{: .notice--warning}`
{: .notice--warning}

**danger** : 빨강 `{: .notice--danger}`
{: .notice--danger}

**success** : 초록 `{: .notice--success}`
{: .notice--success}

## 10-2. 단락안에 마크다운
단락 안에 복잡하게 하고 싶은 말도 있고, 그림도 넣고, 표도 넣고 등등 복잡스럽게 처리하고 싶을 때는 아래 예시 코드를 아예 복사해서 쓴다.

```html
{% raw %}{% capture notice-text %}
여기에 복잡한 내용을 쓴다.
### 제목도 가능
- 목록도 가능
- 목록2

~~~ java
// code 블록도
import class Enum ;
~~~
{% endcapture %}{% endraw %}
<div class="notice--success">{% raw %}{{ notice-text | markdownify }}{% endraw %}</div>
```

{% capture notice-text %}
여기에 복잡한 내용을 쓴다.
### 제목도 가능
- 목록도 가능
- 목록2

~~~ java
// code 블록도
import class Enum ;
~~~
{% endcapture %}
  <div class="notice--success">
    {{ notice-text | markdownify }}
  </div>


## 10-3. extendable

``` html
<details>
  <summary>여기에 제목</summary>
  <div markdown="1">
  {% raw %}{% capture notice-1 %}
내용
  {% endcapture %}
  <div class="notice">
    {{ notice-1 | markdownify }}{% endraw %}
  </div>
  </div>
</details>
```

<details>
  <summary>여기에 제목</summary>
  <div markdown="1">
  {% capture notice-1 %}
내용
  {% endcapture %}

  <div class="notice">
    {{ notice-1 | markdownify }}
  </div>
  </div>
</details>

*****

# 11. 수식입력하기

> [katex 자세한 문법 참고하기](https://katex.org/docs/supported.html)

## 11-1.inline 수식
- '$'로 감싼다.

## 11-2. 수식 block
- '$$'로 감싼다.


# 12. mermaid

- [doc](https://mermaid.js.org/syntax/flowchart.html#a-node-with-round-edges)
- [Editor](https://mermaid-js.github.io/mermaid-live-editor)

<div class="mermaid">
  flowchart LR
    subgraph 원화표시 변액보험 펀드
      direction TB
      A[원화표시 변액보험 펀드] --> B[원화 채권투자]
      A --> C[해외통화 채권투자]
      B --> B1([원화 HW1F])
      C -->|원칙| B1
      C -.->|적합성입증| F([해외통화 HW1F])
      F -.->|"스왑션데이터 부재, 환율시나리오 불가 등"|C3([다른금리모형사용])
      F -->|환율시나리오 가능|F
    end
</div>

<div class="mermaid">
  flowchart LR
    subgraph 해외통화표시 변액보험 펀드
      direction TB
      A1[해외통화표시 변액보험 펀드] --> D[해외통화 채권투자]
      D --> |원칙|E([원화 HW1F])
      D -.-> |적합성입증|F1([해외통화 HW1F])
      F1 -.-> |스왑션 데이터 부재 등|G([다른금리모형 사용])
     end
</div>

> 참고자료   
- [출처](https://gist.github.com/ihoneymon/652be052a0727ad59601)
- [78 Tools for writing and previewing Markdown](http://mashable.com/2013/06/24/markdown-tools/)
- [John gruber 마크다운 번역](http://nolboo.github.io/blog/2013/09/07/john-gruber-markdown/)
- [깃허브 취향의 마크다운 번역](http://nolboo.github.io/blog/2014/03/25/github-flavored-markdown/)
- [허니몬의 마크다운 작성법](http://www.slideshare.net/ihoneymon/ss-40575068)
- Notion.so(<https://www.notion.so/product>)
- Atom(<https://atom.io/>)
- Visual Studio Code(<https://code.visualstudio.com/>)
- Notepad++(<https://notepad-plus-plus.org/>)
