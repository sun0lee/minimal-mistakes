---
title: "Liquid 문법"
categories:
  - blog
tags:
  - blog, liquid
---

출처 : https://heekangpark.github.io/jekyll/06-liquid

# 데이터 타입

1. **String**: 작은따옴표 혹은 큰따옴표로 둘러싸인 문자열. ex. "Hello World!", "a", "3", "false", ...
2. **Number**: 정수 혹은 실수. ex. 3, -2.5, ...
3. **Boolean**: 참 또는 거짓. Boolean 값을 입력할 때 따옴표는 쓰면 안된다(따옴표를 쓰면 String이 된다). ex. true, false
4. **Nil**: 빈 값(Empty value).[^1] 정의되지 않은 변수는 Nil 값을 가지고 있다. Nil을 출력하면 아무것도 나오지 않는다. Nil은 조건문에서 거짓(false)으로 평가된다.
5. **Array**: 배열. 파이썬의 리스트와 유사하게 크기 제약이 없고, 어떠한 타입의 값이든 저장할 수 있다.[^2] 배열의 각 원소는 대괄호(`[`, `]`)에 인덱스 값을 넣어 읽을 수 있다(쓸 수는 없다). 아래에서 나오는 `{% raw %}{% for %}{% endraw %}` 구문 등과 함께 자주 쓰인다.

[^1]: C언어의 `NULL`, 파이썬의 `None`, JS의 `null` 혹은 `undefined`와 같은 개념이다.
[^2]: 하지만 Liquid에서는 빈 배열을 만드는 문법이 없어, 배열을 하나 만드려면 문자열을 잘라서 만드는 간접적인 방법을 써야 한다. 그래서 일반적으로 배열은 문자열 타입만을 담는다. Liquid가 HTML, 마크다운 문서 등을 포멧팅하는 목적으로 쓰인다는 점을 생각한다면, 문자열만 담을 수 있어도 사용하는데 아무 문제 없다.

# 1. 오브젝트 (Object)

오브젝트는 이중 중괄호({% raw %}`{{`, `}}`{% endraw %})로 둘러싸인 코드를 뜻한다. 이 코드는 이중 중괄호 안에 있는 값을 출력한다. C언어의 `printf()` 함수, 파이썬의 `print()` 함수와 유사하다.

{% highlight liquid %}
{% raw %}
{{ "Hello World!" }}
{{ 268.54 }}
{{ false }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Hello World!
268.54
false
{% endhighlight %}

물론, 이렇게 상수를 출력하는 목적으로는 거의 사용하지 않는다. 오브젝트는 일반적으로 변수를 출력하는 목적으로 많이 사용한다.

{% highlight liquid %}
{% raw %}
{% assign text = "Hello World!" %}
{{ text }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Hello World!
{% endhighlight %}

1행의 코드는 `text`라는 변수를 선언하고 그 안에 "Hello World"라는 값을 대입하는 코드이다(자세한 것은 아래 변수 선언문 문단을 참조하자). 이처럼 변수명을 이중 중괄호 사이에 입력하면, 변수가 담고 있는 값이 출력된다.

# 2. 태그 (Tag)

태그는 {% raw %}`{%`, `%}`{% endraw %}으로 둘러싸인 코드를 뜻한다. 몇몇 예외를 제외하고, 대부분의 Liquid 태그는 시작 태그와 종료 태그의 쌍으로 이루어진다. 종료 태그는 시작 태그에 `end`를 붙인 것이다. 예를 들어 조건문 태그의 경우 시작 태그로 `{% raw %}{% if %}{% endraw %}`를 사용하고 종료 태그로 `{% raw %}{% endif %}{% endraw %}`를 사용한다. 시작 태그와 종료 태그는 C언어에서의 중괄호 쌍(`{`, `}`), 파이썬에서의 들여쓰기 문단과 같이, 조건문, 반복문 등이 동작하는 범위를 나타낸다.

태그는 다시 변수 선언문, 조건문, 반복문, 주석문, raw문으로 구분할 수 있다.

## 변수 선언문

지킬에서 변수를 선언하는 방법은 `{% raw %}{% assign %}{% endraw %}` 구문을 이용하는 방법과 `{% raw %}{% capture %}{% endraw %}` 구문을 이용하는 방법, 이렇게 두 가지가 있다.

### {% raw %}{% assign %}{% endraw %} String, Number, Boolean 형 변수를 선언.  
사용 방법은 `=` 기호의 왼편에 변수명, 오른편에 변수에 대입할 값을 넣어주면 된다.

{% highlight liquid %}
{% raw %}
{% assign var1 = "Hello World!" %}
{{ var1 }}

{% assign var2 = -2.835 %}
{{ var2 }}

{% assign var3 = true %}
{{ var3 }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Hello World!
-2.835
true
{% endhighlight %}

### {% raw %}{% capture %}{% endraw %} String 형 변수를 선언.  
사용 방법은 `{% raw %}{% capture %}{% endraw %}` 중괄호 안에 변수명을 입력한 후, `{% raw %}{% capture %}{% endraw %}`와 `{% raw %}{% endcapture %}{% endraw %}` 사이에 변수에 대입할 값을 넣어주면 된다.

{% highlight liquid %}
{% raw %}
{% capture var %}Hello World!{% endcapture %}
{{ var }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Hello World!
{% endhighlight %}

`{% raw %}{% capture %}{% endraw %}`의 강력한 점 중 하나는 다른 변수가 들어간 String으로 변수를 초기화할 수 있다는 것이다. 예를 들어, 아래 예시 코드에서 `var` 변수에는 `Hello! My name is Heekang Park and I'm 26 years old.` 값이 대입되어 있다.

{% highlight liquid %}
{% raw %}
{% assign age = 26 %}
{% assign name = "Heekang Park" %}
{% capture var %}Hello! My name is {{ name }} and I'm {{ age }} years old.{% endcapture %}
{{ var }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Hello! My name is Heekang Park and I'm 26 years old.
{% endhighlight %}

### Nil 타입 변수 초기화

파이썬 등에서는 `x = None`과 같이 하여 빈 값을 명시적으로 선언할 수 있는데, Liquid에서는 Nil 값을 가지는 변수를 명시적으로 선언할 수 없다. 사실 Nil 값을 명시적으로 선언해야 할 일은 거의 일어나지 않기에, 큰 문제가 되진 않는다.

하지만 만약에, 정말 꼭 Nil 값을 사용해야 한다면 선언하지 않은 변수를 사용하는 방법이 있다. 상술했다시피 `{% raw %}{% assign %}{% endraw %}` 혹은 `{% raw %}{% capture %}{% endraw %}`로 선언하지 않은 변수는 Nil 값을 가지고 있기 때문이다.

{% highlight liquid %}
{% raw %}
{{ var }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
(아무 것도 출력되지 않음)
{% endhighlight %}

위 코드처럼 선언되지 변수를 출력하려 하면 아무 값도 출력되지 않는다. 상술했다시피 선언하지 않은 변수는 Nil 값을 가지고 있고, Nil은 출력 시 아무 값도 출력되지 않기 때문이다.

### Array 타입 변수 초기화

Liquid에서는 Array형 변수를 명시적으로 선언할 수 없다. Array형 변수를 선언하려면 우선 String형 변수를 선언한 뒤, split 필터를 이용하는 간접적인 방법을 사용해야 한다. split 필터에 관한 자세한 설명은 아래 [해당 문단](#kramdown_split--문자열로부터-배열-만들기)을 참조하자.

{% highlight liquid %}
{% raw %}
{% assign arr = "Apple,Banana,Tomato" | split: "," %}
{{ arr[0] }}
{{ arr[1] }}
{{ arr[2] }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Apple
Banana
Tomato
{% endhighlight %}

## 조건문

Liquid에서는 `{% raw %}{% if %}{% endraw %}`, `{% raw %}{% unless %}{% endraw %}`, `{% raw %}{% case %}{% endraw %}`, 이렇게 3가지 형태의 조건문을 사용할 수 있다.

### 조건식에서 사용 가능한 연산자

우선 조건문들이 사용하는 조건식에서 사용 가능한 연산자들의 종류를 알아보자. Liquid 조건식에서는 다음과 같은 연산자들을 사용할 수 있다.

- `==` : 같다
- `!=` : 같지 않다
- `>` : (좌항이 우항보다) 크다
- `<` : (좌항이 우항보다) 작다
- `>=` : (좌항이 우항보다) 크거나 같다
- `<=` : (좌항이 우항보다) 작거나 같다
- `contains` : 좌항의 String Array에 우항의 String이 원소로 있는지. 있으면 true, 없으면 false.

또한 조건식에서는 `or`과 `and`를 사용하여 논리합과 논리곱을 각각 표현할 수 있다. Liquid에서는 조건식에 괄호를 쓸 수 없다.[^3] 만약 여러 개의 `and`, `or` 연산자를 사용할 경우, 오른쪽에서 왼쪽 순서로 평가된다. 예를 들어, `true or false and false`는 `true`가 되고[^4], `true and false and false or true`는 `false`가 된다[^5].

[^3]: 괄호를 사용하면 문법 오류가 난다.
[^4]: `true or false and false == true or (false and false) == true or false == true`
[^5]: `true and false and false or true == true and (false and (false or true)) == true and (false and true) == true and false == false`

참고로 Liquid에서는 Nil과 false를 제외한 모든 값들이 `true`로 평가된다.[^6]

[^6]: 빈 String(`""`), 0(Number), 빈 Array도 `true`이다.

### {% raw %}{% if %}{% endraw %}

`{% raw %}{% if %}{% endraw %}`는 다른 프로그래밍 언어와 유사하게 평가할 조건식을 입력하고, 그 조건이 참이면 아래 코드가 실행되는 구문이다.

{% highlight liquid %}
{% raw %}
{% assign score = 100 %}
{% if score > 90 %}
Grade: Pass
{% endif %}

{% assign fruits = "Apple,Banana,Tomato" | split: "," %}
{% if fruits contains "Banana" %}
Banana is in fruits.
{% endif %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Grade: Pass
Banana is in fruits.
{% endhighlight %}

`{% raw %}{% elsif %}{% endraw %}`를 사용하면 `{% raw %}{% if %}{% endraw %}`에 추가적인 조건식을 부여할 수 있다. `{% raw %}{% else %}{% endraw %}` 밑의 코드는 `{% raw %}{% if %}{% endraw %}`의 조건식이 거짓일 때 실행된다.

{% highlight liquid %}
{% raw %}
{% assign score = 100 %}
{% if score > 90 %}
    Grade: A
{% elsif score > 70 %}
    Grade: B
{% else %}
    Grade: Fail
{% endif %}

{% assign score = 50 %}
{% if score > 90 %}
    Grade: A
{% elsif score > 70 %}
    Grade: B
{% else %}
    Grade: Fail
{% endif %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Grade: A
Grade: Fail
{% endhighlight %}

**{% raw %}{% unless %}{% endraw %}**

`{% raw %}{% unless %}{% endraw %}`는 주어진 조건식이 거짓일 때 아래 코드가 실행되는 구문이다. `{% raw %}{% unless %}{% endraw %}`와 정확히 반대로 동작한다.

{% highlight liquid %}
{% raw %}
{% assign height = 190 %}
{% unless height < 180 %}
    Watch your head!
{% endunless %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Watch your head!
{% endhighlight %}

### {% raw %}{% case %}{% endraw %}

`{% raw %}{% case %}{% endraw %}`는 C언어의 switch 구문과 비슷하게 동작한다. 각 분기는 `{% raw %}{% when %}{% endraw %}`으로[^7], 디폴트 분기는 `{% raw %}{% else %}{% endraw %}`를 쓰면 된다[^8].

[^7]: C언어에서는 `case` 키워드를 사용한다.
[^8]: C언어에서는 `default` 키워드를 사용한다.

{% highlight liquid %}
{% raw %}
{% assign name = "Heekang" %}
{% case name %}
    {% when "Heekang" %}
        Hello, Owner!
    {% when "John" %}
        Hello, Friend!
    {% else %}
        Hello, Stranger!
{% endcase %}

{% assign name = "Sarah" %}
{% case name %}
    {% when "Heekang" %}
        Hello, Owner!
    {% when "John" %}
        Hello, Friend!
    {% else %}
        Hello, Stranger!
{% endcase %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Hello, Owner!
Hello, Stranger!
{% endhighlight %}

## 반복문

Liquid에서는 `{% raw %}{% for %}{% endraw %}`를 이용해 반복문을 구성할 수 있다.

### {% raw %}{% for %}{% endraw %}

`{% raw %}{% for %}{% endraw %}`을 이용하면 배열의 원소를 순회할 수 있다.[^9] 예를 들어, 아래 코드는 ["Apple", "Banana", "Tomato"]가 저장되어 있는 Array형 변수 `fruits`의 모든 원소를 출력하는 코드이다.

[^9]: 파이썬의 for 구문과 비슷하다.

{% highlight liquid %}
{% raw %}
{% assign fruits = "Apple,Banana,Tomato" | split: "," %}
{% for fruit in fruits %}
    {{ fruit }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Apple
Banana
Tomato
{% endhighlight %}

위 예시 코드에서 볼 수 있듯이 `{% raw %}{% for %}{% endraw %}` 구문은 변수를 두 개 사용한다. 키워드 `in`을 기준으로, 오른편의 변수(`fruits`)는 순회하고자 하는 배열을 나타낸다. 왼편의 변수는 `{% raw %}{% for %}{% endraw %}`과 `{% raw %}{% endfor %}{% endraw %}` 사이에서만 유효한 지역 변수(local variable)로, 오른편의 Array형 변수의 원소가 앞에서부터 순서대로 하나씩 대입된다.

`{% raw %}{% else %}{% endraw %}`를 이용하면 `{% raw %}{% for %}{% endraw %}`으로 순회하고자 하는 배열에 원소가 하나도 없을 경우 동작하는 폴백(fallback)을 만들 수 있다.

{% highlight liquid %}
{% raw %}
{% assign array = "" | split: "," %}
{% for item in array %}
    {{ item }}
{% else %}
    The array is empty!
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
The array is empty!
{% endhighlight %}

`{% raw %}{% break %}{% endraw %}`, `{% raw %}{% continue %}{% endraw %}`를 이용하면 코드 제어 흐름(control flow)을 조정할 수 있다. 반복문 안에서 `{% raw %}{% break %}{% endraw %}`을 만나면 반복을 중지하고 반복문을 탈출한다. 반복문 안에서 `{% raw %}{% continue %}{% endraw %}`를 만나면 남은 반복 구문의 실행을 생략하고, 다음 원소로 한 걸음 나간 다음 다시 반복 구문을 실행한다.

{% highlight liquid %}
{% raw %}
{% assign fruits = "Apple,Banana,Tomato" | split: "," %}
{% for fruit in fruits %}
    {% if fruit == "Banana" %}
        {% break %}
    {% endif %}

    {{ fruit }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Apple
{% endhighlight %}

{% highlight liquid %}
{% raw %}
{% assign fruits = "Apple,Banana,Tomato" | split: "," %}
{% for fruit in fruits %}
    {% if fruit == "Banana" %}
        {% continue %}
    {% endif %}

    {{ fruit }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Apple
Tomato
{% endhighlight %}

`{% raw %}{% for %}{% endraw %}`와 `{% raw %}{% endfor %}{% endraw %}` 사이에서는 `forloop`라는 이름의 변수에 접근할 수 있다. `forloop` 변수는 다음과 같은 속성(attribute)을 가지고 있다.

- `forloop.first` : 반복문이 첫 번째 반복을 실행 중이면 true, 아니면 false를 반환한다.
- `forloop.index` : 반복문의 반복 횟수를 반환한다.. 첫 번째 반복이면 1, 두 번째 반복이면 2, ...를 반환한다.
- `forloop.index0` : 반복문의 인덱스를 반환한다. 위 `forloop.index`와의 차이점은, `forloop.index`는 1부터 시작하지만 `forloop.index0`는 0부터 시작한다. `forloop.index0` = `forloop.index` - 1이 항상 성립한다.
- `forloop.last` : 반복문이 마지막 반복을 실행 중이면 true, 아니면 false를 반환한다.
- `forloop.length` : 반복문의 전체 반복 횟수를 반환한다.
- `forloop.rindex` : 역순으로의 `forloop.index`를 반환한다. `forloop.index` + `forloop.rindex` = `forloop.length` + 1이 항상 성립한다.
- `forloop.rindex0` : 역순으로의 `forloop.index0`를 반환한다. `forloop.index0` + `forloop.rindex0` = `forloop.length` - 1, `forloop.rindex0` = `forloop.rindex` - 1이 항상 성립한다.

{% highlight liquid %}
{% raw %}
{% assign numbers = "1,2,3,4,5" | split: "," %}
{% for number in numbers %}
    number = {{ number }}
    forloop.first = {{ forloop.first }}
    forloop.index = {{ forloop.index }}
    forloop.index0 = {{ forloop.index0 }}
    forloop.last = {{ forloop.last }}
    forloop.length = {{ forloop.length }}
    forloop.rindex = {{ forloop.rindex }}
    forloop.rindex0 = {{ forloop.rindex0 }}
    ===============================
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
number = 1
forloop.first = true
forloop.index = 1
forloop.index0 = 0
forloop.last = false
forloop.length = 5
forloop.rindex = 5
forloop.rindex0 = 4
===============================

number = 2
forloop.first = false
forloop.index = 2
forloop.index0 = 1
forloop.last = false
forloop.length = 5
forloop.rindex = 4
forloop.rindex0 = 3
===============================

number = 3
forloop.first = false
forloop.index = 3
forloop.index0 = 2
forloop.last = false
forloop.length = 5
forloop.rindex = 3
forloop.rindex0 = 2
===============================

number = 4
forloop.first = false
forloop.index = 4
forloop.index0 = 3
forloop.last = false
forloop.length = 5
forloop.rindex = 2
forloop.rindex0 = 1
===============================

number = 5
forloop.first = false
forloop.index = 5
forloop.index0 = 4
forloop.last = true
forloop.length = 5
forloop.rindex = 1
forloop.rindex0 = 0
===============================
{% endhighlight %}

`limit`를 사용하면 반복할 횟수를 제한할 수 있다. 반복문은 `limit`로 제한한 횟수만큼만 딱 실행되고 반복을 종료한다.

{% highlight liquid %}
{% raw %}
{% assign numbers = "1,2,3,4,5" | split: "," %}
{% for number in numbers limit: 3 %}
    {{ number }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
1
2
3
{% endhighlight %}

`offset`를 사용하면 반복을 시작할 인덱스 위치를 정할 수 있다. `offset` 값 이하 인덱스의 값들은 스킵된다. 인덱스는 0부터 시작함을 주의하자. 즉, `offset`으로 2를 주면, 인덱스 2(3번째 원소)부터 반복이 시작된다.

{% highlight liquid %}
{% raw %}
{% assign numbers = "1,2,3,4,5" | split: "," %}
{% for number in numbers offset: 2 %}
    {{ number }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
3
4
5
{% endhighlight %}

`reversed`를 사용하면 반복의 방향을 역순으로 할 수 있다.

{% highlight liquid %}
{% raw %}
{% assign numbers = "1,2,3,4,5" | split: "," %}
{% for number in numbers reversed %}
    {{ number }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
5
4
3
2
1
{% endhighlight %}

`limit`, `offset`, `reversed`는 혼용 가능하다. 이때, `reversed`는 반드시 Array 변수 바로 옆에 와야 하고[^10], `limit`과 `offset`의 순서는 어떠한 순서든 모두 허용된다. 또한 `reversed`는 `limit`, `offset` 등이 적용된 이후 가장 마지막에 적용된다.

[^10]: 예를 들어, `{% raw %}{% for number in numbers reversed offset: 2 limit: 3 %}{% endraw %}`는 되지만, `{% raw %}{% for number in numbers offset: 2 limit: 3 reversed %}{% endraw %}`는 문법 오류가 발생한다.

{% highlight liquid %}
{% raw %}
{% assign numbers = "1,2,3,4,5" | split: "," %}
{% for number in numbers reversed offset: 2 %}
    {{ number }}
{% endfor %}

{% assign numbers = "1,2,3,4,5" | split: "," %}
{% for number in numbers reversed offset: 2 limit: 2 %}
    {{ number }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
5
4
3

4
3
{% endhighlight %}

`{% raw %}{% for %}{% endraw %}`에서는 두 숫자 범위(range)를 반복할 수도 있다. 시작값 `start`와 종료값 `end`를 `(start..end)` 꼴로 `in` 오른편에 적어 주면 된다. 파이썬의 `range()`와 유사한데, 중요한 차이점은 반복의 범위가 `start` 이상 `end` **이하**라는 것이다.[^11] `start`와 `end`는 음수일 수도 있지만, 반드시 `end`가 `start`보다 커야 한다. `start`와 `end`에는 변수를 쓸 수도 있다. 다음 예시 코드를 참조하자.

[^11]: 파이썬에서는 `start` 이상, `end` **미만**의 범위에서 반복한다.

{% highlight liquid %}
{% raw %}
{% assign fruits = "Apple,Banana,Tomato,Melon,Kiwi" | split: "," %}
{% assign start = 2 %}
{% for number in (start..5) %}
    number = {{ number }}
    fruits[number] = {{ fruits[number] }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
number = 2
fruits[number] = Tomato

number = 3
fruits[number] = Melon

number = 4
fruits[number] = Kiwi

number = 5
fruits[number] =
{% endhighlight %}

위 예제에서는 마지막 반복에서 `fruits`에서 존재하지 않는 인덱스 5번 원소에 접근하였기에 Nil(아무 값도 출력되지 않음)이 출력되었다.

당연히 `(start..in)`에 대해서도 `reversed`, `offset`, `limit`를 쓸 수 있다.

{% highlight liquid %}
{% raw %}
{% for number in (1..5) reversed offset: 2 limit: 3 %}
    {{ number }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
5
4
3
{% endhighlight %}

## 기타 구문

**주석문**

Liquid에서 주석은 다음과 같이 `{% raw %}{% comment %}{% endraw %}` 구문을 이용한다.

{% highlight liquid %}
{% raw %}
{% comment %}
Everything between comment tags are not interpreted.
{% endcomment %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
(아무것도 출력되지 않음)
{% endhighlight %}

Liquid가 해석될 때 모든 주석은 삭제된다. 주석 안에 마크다운 문장, HTML 구문 등 어떠한 값을 입력해도 모두 출력되지 않는다([지킬 렌더링 순서](/jekyll/05-rendering-order) 문서 참조).

**Raw문**

Liquid는 Liquid의 문법을 구성하는 {% raw %}`{{`, `}}`, `{%`, `%}`{% endraw %} 기호들을 보면 이를 최대한 해석해보려 한 후, 문법 오류가 있다면 해당 문장의 해석을 건너뛰고(즉, 렌더링하지 않고) 넘어간다. 따라서, 이런 기호를 사용하고 싶으면 Liquid 엔진이 건드리지 않도록 이스케이프 처리가 필요하다. 이럴 때 쓰는 것이 `{% raw %}{% raw %}{% endraw %}` 구문이다. 참고로, Liquid 문법을 설명하는 이 문서에도 (당연히) 아주 많은 `{% raw %}{% raw %}{% endraw %}`가 사용되었다.

{% highlight liquid %}
{% raw %}{% raw %}{% endraw %}
{%- raw -%}
    {% assign fruits = "Apple,Banana,Tomato" | split: "," %}
    {% for fruit in fruits %}
        {{ fruit }}
    {% endfor %}
{% endraw %}
{%- assign temp = "{%" -%}
{{ temp }} endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
{% raw %}
{% assign fruits = "Apple,Banana,Tomato" | split: "," %}
{% for fruit in fruits %}
    {{ fruit }}
{% endfor %}
{% endraw %}
{% endhighlight %}

# 3.필터 (Filter)

필터란 오브젝트 또는 태그에 추가적으로 사용되어져, 출력 결과를 바꾸는 문법 요소이다. 필터는 다음과 같이 사용한다.

{% highlight liquid %}
{% raw %}
{{ "Hello" | append: " World!" }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Hello World!
{% endhighlight %}

위 코드는 [append 필터](#kramdown_append--string-뒤에-붙이기)를 사용해 문자열 "Hello"와 문자열 "World!"를 이어 붙이는 코드이다. 이때 "Hello"를 입력값(Input Value), "World!"를 인자값(Argument)이라 한다. 모든 필터에는 반드시 입력값이 있어야 하며, 인자값은 없거나 최대 2개까지 있을 수 있다. 필터는 `|` 기호를 이용해[^12] 오브젝트 혹은 태그에 적용 가능하다. 또한 마치 리눅스 쉘에서 `|` 기호로 여러 개의 명령어를 이어 붙일 수 있듯이(파이프라이닝), Liquid에서도 유사하게 `|` 기호를 계속 연결해 여러 개의 필터를 연속적으로 동시에 적용할 수도 있다.

[^12]: 몇몇 필터의 경우 `.` 기호로 적용할 수도 있다.

{% highlight liquid %}
{% raw %}
{{ "Hello" | append: " World!" | append: " I love " | append: "you!" }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Hello World! I love you!
{% endhighlight %}

Liquid는 다양한 종류의 필터를 지원한다. 필터는 Liquid를 잘 다루기 위한 필수적인 도구이므로 익숙해 지도록 하자.

**abs : 절대값**

abs 필터는 입력값의 절대값을 반환하는 필터이다.

{% highlight liquid %}
{% raw %}
{{ -10 | abs }}

{% assign x = -35.123 | abs %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
10
35.123
{% endhighlight %}

만약 Number 타입이 아닌 값에 abs 필터를 씌우면 0이 출력된다.

{% highlight liquid %}
{% raw %}
{{ "String" | abs }}

{{ true | abs }}

{% assign array = "1,2,3" | split: "," %}
{{ array | abs }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
0
0
0
{% endhighlight %}

**append : 문자열 뒤에 붙이기**

append 필터는 입력값 뒤에 필터의 인자값을 붙여 하나의 문자열을 만들어 반환하는 필터이다. 이때 입력값은 어떠한 데이터 타입이든 상관 없으나(모두 String으로 자동 변환되어 사용된다), 인자값은 반드시 String 타입이어야 한다(즉, 반드시 따옴표(`"`)로 묶여 있어야 한다).

{% highlight liquid %}
{% raw %}
{{ "Hello" | append: "World!" }}

{% assign path = "/jekyll" | append: "/06-liquid" %}
{{ path }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
HelloWorld!
/jekyll/06-liquid
{% endhighlight %}

**at_least : 출력되는 변수의 하한 정하기**

at_least 필터는 변수를 출력할 때 그 하한을 지정할 수 있는 필터이다. 즉 입력값이 인자값보다 크거나 같은 경우에는 입력값을 그대로 출력하지만, 입력값이 인자값보다 작다면 인자값이 출력된다. 입력값, 인자값이 Number 타입이 아닌 경우 0으로 평가된다.

{% highlight liquid %}
{% raw %}
{{ 5 | at_least: 3 }}
{{ 1 | at_least: 3 }}

{% assign x = -10 | at_least: -2.375 %}
{{ x }}

{% assign y = 1 | at_least: -2.375 %}
{{ y }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
5
3
-2.375
1
{% endhighlight %}

**at_most : 출력되는 변수의 상한 정하기**

at_most 필터는 변수를 출력할 때 그 상한을 지정할 수 있는 필터이다. 즉 입력값이 인자값보다 작거나 같은 경우에는 입력값을 그대로 출력하지만, 입력값이 인자값보다 크다면 인자값이 출력된다. 입력값, 인자값이 Number 타입이 아닌 경우 0으로 평가된다.

{% highlight liquid %}
{% raw %}
{{ 5 | at_most: 3 }}
{{ 1 | at_most: 3 }}

{% assign x = -10 | at_most: -2.375 %}
{{ x }}

{% assign y = 1 | at_most: -2.375 %}
{{ y }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
3
1
-10
-2.375
{% endhighlight %}

**capitalize : 첫 글자 대문자로, 나머지는 소문자로**

capitalize 필터는 입력값의 첫 글자를 대문자로, 나머지는 소문자로 만드는 필터이다. 만약 입력값이 String이 아니라면 String으로 자동 변환되어 처리된다.

{% highlight liquid %}
{% raw %}
{{ "hello World!" | capitalize }}

{% assign x = "hELLO WORLD!" | capitalize %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Hello world!
Hello world!
{% endhighlight %}

**ceil : 정수로 올림**

ceil 필터는 입력값을 정수로 올림연산하는 필터이다. 만약 입력값이 Number가 아니라면 최대한 Number로 변환하여 해석하려 한다. 변환에 실패하면 0으로 간주한다.

{% highlight liquid %}
{% raw %}
{{ 1.2 | ceil }}
{{ -2.7 | ceil }}
{{ 3.0 | ceil }}

{% assign x = "123.456" | ceil %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
2
-2
3

124
{% endhighlight %}

**compact : 배열에서 Nil 값 제거하기**

compact 필터는 입력값 Array에서 Nil값을 제거하는 필터이다. 만약 입력값이 Array가 아니거나, Array에 Nil값이 없다면 아무 일도 일어나지 않는다.

{% highlight liquid %}
{% raw %}
{% assign array = "1,2,3,4" | split: "," | push: x | push: "5" %}
array.size = {{ array | size }}
{% for item in array %}
  - {{ item }}
{% endfor %}

{% assign array = array | compact %}
array.size = {{ array | size }}
{% for item in array %}
  - {{ item }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
array.size = 6
- 1
- 2
- 3
- 4
-
- 5

array.size = 5
- 1
- 2
- 3
- 4
- 5
{% endhighlight %}

위 예시 코드는 Liquid 문법에 익숙하지 않다면 조금 어렵게 느껴질 수도 있다. 위 코드는 다음과 같은 일을 하는 코드이다: 우선 [split 필터](#kramdown_split--문자열로부터-배열-만들기)를 이용해 ["1", "2", "3", "4"]가 저장된 배열 `array`를 만들었다. 그리고 [push 필터](#kramdown_push)를 이용해 `array` 안에 정의되지 않은 변수 `x`와 String 변수 "5"를 추가하였다. 정의되지 않은 변수에는 Nil이 저장되어 있으므로, 첫 번째 줄의 실행 결과 `array` 안에는 ["1", "2", "3", "4", Nil, "5"]가 저장되게 된다.

이후 size 필터를 이용해 `array`의 크기를 출력하였다. 현재 `array` 안에는 총 6개의 원소가 있으므로 6이 출력되었다. 그리고 `{% raw %}{% for %}{% endraw %}`을 이용해 `array` 안의 원소를 하나씩 출력해 보았다. Nil은 출력 시 아무 값도 나오지 않으므로, 위 출력 예시와 같이 아무것도 출력되지 않은 행이 존재한다.

이후 compact 필터를 적용해 `array` 안에서 Nil값을 모두 제거하였다(["1", "2", "3", "4", "5"]). 그 결과 `array`의 크기는 5가 되었고, 각 원소를 출력할 때 (Nil 값이 없으므로) 빈 줄이 출력되지 않는다.

**concat : 배열 합치기**

concat 필터는 두 개의 배열을 합치는 필터이다. 다른 언어에서 일반적으로 "concatenate"라는 단어를 문자열을 합친다는 뜻으로 많이 사용해 헷갈릴 수 있는데, Liquid에서 문자열을 합치기 위해서는 append 혹은 prepend 필터를 사용해야 한다. 만약 인자값이 Array가 아닐 경우 오류가 발생한다.

{% highlight liquid %}
{% raw %}
{% assign boys = "John,Mike,Tim,James,Harry" | split: "," %}
{% assign girls = "Sarah,Lucy,Mindy,Emma,Luna" | split: "," %}

{% assign students = boys | concat: girls %}
{% for student in students %}
  - {{ student }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
- John
- Mike
- Tim
- James
- Harry
- Sarah
- Lucy
- Mindy
- Emma
- Luna
{% endhighlight %}

**date : 날짜 포멧팅**

date 필터는 입력값 날짜를 포멧팅하는 필터이다. 입력값은 루비의 [Time.parse() 메소드](https://ruby-doc.org/stdlib/libdoc/time/rdoc/Time.html#method-c-parse)가 사용하는 것과 동일한 포멧이어야 한다. 대충 웬만하게 상식적인 날짜 표기법은 다 사용 가능하다. 입력값으로 "now" 혹은 "today"를 입력할 경우 현재 시간을 가져와 사용한다.[^13]

[^13]: 혹시나 싶어 사족을 달자면, 지킬은 **정적** 사이트 생성기이다. "now" 혹은 "today"는 빌드 시점에서의 현재 시간을 사용한다. 동적 사이트처럼 사용자가 웹 페이지에 접속할 때마다 현재 시간을 출력하는 것이 아니다.

{% highlight liquid %}
{% raw %}
{{ "2018-12-31" | date: "%a, %b %d, %y" }}
{{ "now" | date: "%Y-%m-%d %H:%M" }}
{{ "April 1, 2015" | date: "%a" }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Thu, Dec 31, 18
2020-12-17 01:48
Wed
{% endhighlight %}

인자값에 사용 가능한 포멧 키워드 목록은 다음과 같다.

- 연도
  - `%C` : 4자리 수 연도의 앞 2자리[00-99]. 이 값에 1을 더하면 세기(Century)가 된다.
  - `%Y` : 연도[0000-9999]
  - `%y` : 연도[00-99]. 4자리 수 연도의 뒤 2자리(ex. 1234년의 34). 참고로 `%C%y`는 `%Y`와 같다.
- 월
  - `%m` : 월[01-12]. 한 자리수 월의 경우 앞에 0이 붙어 출력된다.
  - `%b` : 월의 영어 축약형 이름[Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec]
  - `%B` : 월의 영어 이름[January, February, March, April, May, June, July, August, September, October, November, December]
- 주 번호
  - `%V` : ISO 주 번호[01-53]. 월요일을 한 주의 시작으로 하여 카운트한다. 한 자리수 주차의 경우 앞에 0이 붙어 출력된다. 만약 특정 연도의 1월 1일이 있는 주가 4일 이상을 포함하면[^14] 1월 1일이 있는 주를 해당 년도의 첫 번째(01) 주차로 카운트한다. 만약 그렇지 않으면[^15] 1월 1일이 있는 주는 작년의 마지막 주차로 카운트되고, 그 다음 월요일부터가 해당 년도의 첫 번째 주차가 된다.
  - `%W` : 주 번호[00-53]. 월요일을 한 주의 시작으로 하여 카운트한다. 한 자리수 주차의 경우 앞에 0이 붙어 출력된다. 연도의 첫 번째 월요일이 있는 주의 주 번호가 01이 되고, 해당 년도의 그 이전 날짜들은 주 번호로 00을 쓴다.
  - `%U` : 주 번호[00-53]. 일요일을 한 주의 시작으로 하여 카운트한다. 한 자리수 주차의 경우 앞에 0이 붙어 출력된다. 연도의 첫 번째 일요일이 있는 주의 주 번호가 01이 되고, 해당 년도의 그
  이전 날짜들은 주 번호로 00을 쓴다.
- 일
  - `%d` : 일[01-31]. 한 자리수 일의 경우 앞에 0이 붙어 출력된다.
  - `%e` : 일[1-31]. 한 자라수 일의 경우 그대로 한 자리수로 출력된다.
  - `%j` : 연도의 일[001-366]
- 요일
  - `%a` : 요일의 영어 축약형 이름(3글자)[Mon, Tue, Wed, Thu, Fri, Sat, Sun]
  - `%A` : 요일의 영어 이름[Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday]
  - `%w` : 요일[0-6]. 요일을 숫자로 매칭한 값이 출력된다. 일요일은 0, 월요일은 1, 화요일은 2, 수요일은 3, 목요일은 4, 금요일은 5, 토요일은 6이다.
  - `%u` : 요일[1-7]. 요일을 숫자로 매칭한 값이 출력된다. 월요일은 1, 화요일은 2, 수요일은 3, 목요일은 4, 금요일은 5, 토요일은 6, 일요일은 7이다.
- 시
  - `%H` : 24시간제의 시[00-23]. 한 자리수 시의 경우 앞에 0이 붙어 출력된다.
  - `%k` : 24시간제의 시[0-23]. 한 자리수 시의 경우 그대로 한 자리수로 출력된다.
  - `%I` : 12시간제의 시[01-12]. 한 자리수 시의 경우 앞에 0이 붙어 출력된다.
  - `%l` : 12시간제의 시[01-12]. 한 자리수 시의 경우 그대로 한 자리수로 출력된다.
- 분
  - `%M` : 분[00-59]. 한 자리수 분의 경우 앞에 0이 붙어 출력된다.
- 초
  - `%S` : 초[00-61]. 한 자리수 초의 경우 앞에 0이 붙어 출력된다. 윤초의 경우 60, 이중 윤초의 경우 61이 출력된다.
  - `%s` : POSIX 시간. 1970년 1월 1일 00:00:00부터 경과한 시간을 초로 환산한 것.
- 밀리초
  - `%L` : 밀리초[000-999]. 한 자리수, 두 자리수 밀리초의 경우 각각 앞에 00, 0이 붙어 출력된다.
- AM/PM
  - `%p` : AM/PM[AM, PM]
  - `%P` : AM/PM[am, pm]
- 시간대
  - `%z` : UTC 오프셋[+HHMM, -HHMM]. +는 GMT 동쪽, -는 GMT 서쪽을 의미하고, HH는 GMT에서의 시간 수, MM은 GMT에서의 분 수를 의미한다.
- 축약형
  - `%D` : `%m/%d/%y`의 축약형
  - `%v` : `%e-%b-%Y`의 축약형
  - `%F` : ISO 날짜 포멧. `%Y-%m-%d`의 축약형.
  - `%r` : 12시간제 시간 포멧. `%I:%M:%S %p`의 축약형.
  - `%R` : 24시간제 시간 포멧(초 없음). `%H:%M`의 축약형.
  - `%T` : 24시간제 시간 포멧. `%H:%M:%S`의 축약형.

[^14]: 즉, 1월 1일이 월, 화, 수, 목 중 하나이면
[^15]: 즉, 1월 1일이 금, 토, 일 중 하나이면

**default : 디폴트 값 지정**

default 필터는 디폴트 값을 지정하는 필터이다. 인자값에 사용할 디폴트 값을 입력하면 된다. 디폴트 값은 입력값이 Nil, false, ""(빈 문자열)인 경우 적용된다.

{% highlight liquid %}
{% raw %}
{{ x | default: "Not Defined!" }}
{{ false | default: 1234 }}

{% assign text = "" %}
{{ x | default: "Empty String" }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Not Defined!
1234
Empty String
{% endhighlight %}

**divided_by : 나눗셈**

divided_by 필터는 입력값을 인자값으로 나누는 필터이다. 입력값과 인자값에는 Number 타입의 값을 사용해야 한다. 만약 Number 타입이 아닌 값이 사용되면 최대한 Number로 해석하려 하고, 실패하면 0으로 간주한다. (당연히) 인자값은 0이면 안 된다.

{% highlight liquid %}
{% raw %}
{{ 16 | divided_by: 4 }}

{% assign x = 25 | divided_by: 5 %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
4
5
{% endhighlight %}

C언어에서 `/` 기호로 나눗셈을 할 때면 주어진 값이 정수형인지 실수형인지에 따라 결과가 달라진다. 정수형끼리의 나눗셈은 정수 나눗셈을 수행하고(= 정수가 나오고 = 몫을 계산하고), 정수형과 실수형, 또는 실수형과 실수형 간의 나눗셈은 실수 나눗셈을 수행한다(= 실수가 나온다). divided_by 필터도 동일하게 작동한다. Number 타입 역시 정수값와 실수값을 사용할 수 있는데, 이때 정수값과 정수값 간의 연산은 정수로, 정수값과 실수값, 실수값과 실수값 사이의 연산은 실수로 계산된다.

{% highlight liquid %}
{% raw %}
{{ 5 | divided_by: 2 }}
{{ 5.0 | divided_by: 2 }}
{{ 5 | divided_by: 2.0 }}
{{ 5.0 | divided_by: 2.0 }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
2
2.5
2.5
2.5
{% endhighlight %}

참고로 Liquid에는 정수값을 실수값으로 전환하는 필터가 없다.[^16] 만약 정수값을 실수값으로 바꾸고 싶다면 다음과 같이 times 필터를 사용하는 편법을 사용해야 한다.

[^16]: 실수값에서 정수값으로의 전환은 ceil 필터를 사용하면 된다.

{% highlight liquid %}
{% raw %}
{{ 5 | times: 1.0 }}
{{ 5 | times: 1.0 | divided_by: 2 }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
5.0
2.5
{% endhighlight %}

**downcase : 소문자로**

downcase 필터는 입력값을 소문자로 바꾸는 필터이다. 만약 입력값이 String이 아니라면 String으로 자동 변환되어 처리된다.

{% highlight liquid %}
{% raw %}
{{ "HELLO WORLD!" | downcase }}

{% assign x = "hElLo WoRlD!" | downcase %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
hello world!
hello world!
{% endhighlight %}

**escape : 이스케이핑**

escape 필터는 입력값 문자열을 이스케이핑(escaping) 하는 필터이다. 이스케이핑된 문자열은 URL 등에 사용할 수 있다. 이스케이핑할 문자열이 없다면 아무 일도 일어나지 않는다. 만약 입력값이 String이 아니라면 String으로 자동 변환되어 처리된다.

{% highlight liquid %}
{% raw %}
{{ "I love 'Harry Potter', written by 'Joanne K. Rowling'!" | escape }}

{% assign url = "/you/might/want/to/click/this&that" | escape %}
{{ url }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
I love &#39;Harry Potter&#39;, written by &#39;Joanne K. Rowling&#39;!
/you/might/want/to/click/this&amp;that
{% endhighlight %}

**escape_once : 이스케이핑**

escape_once 필터는 입력값 문자열을 이스케이핑(escaping) 하는 필터이다. escape_once 필터는 [escape 필터](#kramdown_escape--이스케이핑)와 같은 역할을 하지만, 한 가지 차이점이 있다. 만약 주어진 입력값이 이미 이스케이핑 된 문자열일 경우 escape_once는 이스케이핑하지 않는다. 반면 escape 필터의 경우 이스케이핑되어 나온 특수문자(ex. `&`, `;` 등)를 다시 이스케이핑하여 이스케이핑이 깨진다. 만약 이미 이스케이핑 된 문장을 다시 이스케이핑을 해야 할 일이 생긴다면 escape_once 필터를 사용하도록 하자. 이스케이핑되지 않은 문장을 이스케이핑하는 곳에는 escape 필터와 escape_once 필터 어느 것을 사용해도 동일하다.

{% highlight liquid %}
{% raw %}
{{ "1 < 2 & 3" | escape }}
{{ "1 < 2 & 3" | escape | escape }}

{{ "1 < 2 & 3" | escape_once }}
{{ "1 < 2 & 3" | escape_once | escape_once }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
1 &lt; 2 &amp; 3
1 &amp;lt; 2 &amp;amp; 3

1 &lt; 2 &amp; 3
1 &lt; 2 &amp; 3
{% endhighlight %}

**first : 배열의 첫 번째 요소 반환**

first 필터는 입력값으로 전달받은 Array형 값의 첫 번째 요소를 반환하는 필터이다. Array형 변수 `array`가 주어졌다고 했을 때, `array`에 first 필터를 사용하는 것과 `array[0]`은 완벽히 동일하다.

만약 배열의 원소가 없다면 Nil 값이 출력된다. 입력값이 Array형 변수가 아닐 경우에도 Nil값이 출력된다.

first 필터의 경우 `|` 기호 말고도 `.`을 이용해 사용할 수도 있다.

{% highlight liquid %}
{% raw %}
{% assign array = "Apple,Banana,Tomato" | split: "," %}

{{ array | first }}
{{ array.first }}
{{ array[0] }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Apple
Apple
Apple
{% endhighlight %}

**floor : 정수로 버림**

floor 필터는 입력값을 정수로 버림연산하는 필터이다. 만약 입력값이 Number가 아니라면 최대한 Number로 변환하여 해석하려 한다. 변환에 실패하면 0으로 간주한다.

{% highlight liquid %}
{% raw %}
{{ 1.2 | floor }}
{{ -2.7 | floor }}
{{ 3.0 | floor }}

{% assign x = "123.456" | floor %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
1
-3
3

123
{% endhighlight %}

**join : 배열을 문자열로 바꾸기**

join 필터는 배열의 각 요소들을 이어 붙여 하나의 문자열로 바꾸는 필터이다. join 필터가 전달받은 값은 문자열을 만들 때 각 원소 사이에 삽입된다. 인자값이 없다면 `" "`(공백)을 디폴트로 삽입한다.

{% highlight liquid %}
{% raw %}
{% assign array = "Apple,Tomato,Banana" | split: "," %}

{{ array | join }}
{{ array | join: ","}}
{{ array | join: " and " }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Apple Tomato Banana
Apple,Tomato,Banana
Apple and Tomato and Banana
{% endhighlight %}

**last : 배열의 마지막 요소 반환**

last 필터는 입력값으로 전달받은 Array형 값의 마지막 요소를 반환하는 필터이다.

만약 배열의 원소가 없다면 Nil 값이 출력된다. 입력값이 Array형 변수가 아닐 경우에도 Nil값이 출력된다.

last 필터의 경우 `|` 기호 말고도 `.`을 이용해 사용할 수도 있다.

{% highlight liquid %}
{% raw %}
{% assign array = "Apple,Banana,Tomato" | split: "," %}

{{ array | last }}
{{ array.last }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Tomato
Tomato
{% endhighlight %}

**lstrip : 왼쪽 공백 제거**

lstrip 필터는 입력값의 왼쪽 모든 공백(Whitespace)[^17]을 제거하는 필터이다. 공백 문자가 아닌 글자 사이에 있는 (정상적인) 공백은 제거되지 않는다.

[^17]: 탭(tab), 띄어쓰기(space), 개행(newline) 등

{% highlight liquid %}
{% raw %}
//////{{ "                 Hello     World!" | lstrip }}//////

{% assign x = "                 Hello     World!        " | lstrip %}
//////{{ x }}//////
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
//////Hello     World!//////
//////Hello World!        //////
{% endhighlight %}

**map : 하위 속성 추출하여 배열 만들기**

map 필터는 입력값 배열의 모든 요소로부터 하위 속성(attribute)을 추출해 하나의 배열로 만들어주는 필터이다.

`site.collections`는 사이트의 모든 컬렉션들의 배열이다. 그리고 본 블로그에서 컬렉션들은 모두 컬렉션 이름을 가지고 있는 하위 속성 `name`이 있다.

{% highlight liquid %}
{% raw %}
{% for collection in site.collections %}
  - {{ collection.name }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
- 미적분학 (Calculus)
- 기타 (Etc)
- Git
- Javascript
- 지킬 (Jekyll)
- 기계학습 (Machine Learning)
- NAS
- Numpy
- Re : 제로부터 배우는 파이썬
- Oracle VM VirtualBox
- 웹 서버 (Web Server)
{% endhighlight %}

이때, map 필터를 이용하면 다음과 같이 모든 컬렉션들에서 `name` 속성을 뽑아 배열 `names`를 만들 수 있다.

{% highlight liquid %}
{% raw %}
{% assign names = site.collections | map: "name" %}

{% for name in names %}
  - {{ name }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
- 미적분학 (Calculus)
- 기타 (Etc)
- Git
- Javascript
- 지킬 (Jekyll)
- 기계학습 (Machine Learning)
- NAS
- Numpy
- Re : 제로부터 배우는 파이썬
- Oracle VM VirtualBox
- 웹 서버 (Web Server)
{% endhighlight %}

Liquid에서는 배열을 원하는 대로 초기화할 수 없고, 하위 속성을 마음대로 추가/삭제할 수 없다. 또한 map 필터로 할 수 있는 일들은 거의 대부분 `{% raw %}{% for %}{% endraw %}` 태그를 이용하여 똑같이 할 수 있다. 그래서 필자의 경우 map 필터를 잘 사용하지 않는다.

**minus : 뺄셈**

minus 필터는 입력값에서 인자값을 빼는 필터이다. 입력값과 인자값에는 Number 타입의 값을 사용해야 한다. 만약 Number 타입이 아닌 값이 사용되면 최대한 Number로 해석하려 하고, 실패하면 0으로 간주한다.

{% highlight liquid %}
{% raw %}
{{ 16 | minus: 4 }}

{% assign x = 5.5 | minus: 20 %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
12
-14.5
{% endhighlight %}

다른 언어에서는 `+`, `-`, `*`, `/`, `%` 기호로 사칙연산이 바로 가능하다. 예를 들어 파이썬에서 `x = 5 - 3`이라 하면 5 - 3이 계산되어 `x`에 2가 저장된다. 하지만 Liquid에서는 사칙연산을 하기 위해서 반드시 [plus](#kramdown_plus--덧셈), minus, [times](#kramdown_times--곱셈), [divided_by](#kramdown_divided_by--나눗셈), [modulo](#kramdown_modulo--나머지셈)와 같은 필터를 반드시 사용해야 한다.

예를 들어 배열 `array`가 주어졌을 때, 인덱스 `i`의 직전 요소를 접근하는 상황을 생각해 보자. 이때 `{% raw %}{{ array[i - 1] }}{% endraw %}`와 같은 구문은 문법 오류가 난다. 제대로 작동하게 하려면 아래 코드와 같이 대괄호 밖에서 minus 필터를 이용해 1을 뺀 후 그 값을 대괄호 안에 넣어야 한다.

{% highlight liquid %}
{% raw %}
{% assign array = "Apple,Banana,Tomato" | split: "," %}
{% assign i = 1 %}

{% assign prev = i | minus: 1 %}
{{ array[prev] }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Apple
{% endhighlight %}

**modulo : 나머지셈**

modulo 필터는 입력값을 인자값으로 나눈 나머지를 구하는 필터이다. 입력값과 인자값에는 Number 타입의 값을 사용해야 한다. 만약 Number 타입이 아닌 값이 사용되면 최대한 Number로 해석하려 하고, 실패하면 0으로 간주한다. (당연히) 인자값은 0이면 안 된다. 또한 modulo 필터는 입력값과 인자값에 음수, 실수가 들어와도 문법 오류를 내지 않으므로 조심하자.

{% highlight liquid %}
{% raw %}
{{ 17 | modulo: 4 }}

{% assign x = 27 | divided_by: 5 %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
1
2
{% endhighlight %}

**newline_to_br : 개행문자 &lt;br/&gt;로 바꾸기**

newline_to_br 필터는 입력값 문자열의 개행문자(`\n`)를 &lt;br/&gt;로 바꾸는 필터이다.

{% highlight liquid %}
{% raw %}
{% capture string %}동해물과 백두산이 마르고 닳도록
하느님이 보우하사 우리나라 만세
무궁화 삼천리 화려강산
대한사람 대한으로 길이 보전하세{% endcapture %}

<div>{{ string }}</div>

<div>{{ string | newline_to_br }}</div>
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
<div>동해물과 백두산이 마르고 닳도록
하느님이 보우하사 우리나라 만세
무궁화 삼천리 화려강산
대한사람 대한으로 길이 보전하세</div>

<div>동해물과 백두산이 마르고 닳도록<br />
하느님이 보우하사 우리나라 만세<br />
무궁화 삼천리 화려강산<br />
대한사람 대한으로 길이 보전하세</div>
{% endhighlight %}

**plus : 덧셈**

plus 필터는 입력값에 인자값을 더하는 필터이다. 입력값과 인자값에는 Number 타입의 값을 사용해야 한다. 만약 Number 타입이 아닌 값이 사용되면 최대한 Number로 해석하려 하고, 실패하면 0으로 간주한다.

{% highlight liquid %}
{% raw %}
{{ 16 | plus: 4 }}

{% assign x = -5.5 | plus: 20 %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
20
-14.5
{% endhighlight %}

**prepand : 문자열 앞에 붙이기**

prepand 필터는 입력값 앞에 필터의 인자값을 붙여 하나의 문자열을 만들어 반환하는 필터이다. 이때 입력값은 어떠한 데이터 타입이든 상관 없으나(모두 String으로 자동 변환되어 사용된다), 인자값은 반드시 String 타입이어야 한다(즉, 반드시 따옴표(`"`)로 묶여 있어야 한다).

{% highlight liquid %}
{% raw %}
{{ "$20" | prepend: "Apple : " }}

{% assign baseurl = "/jekyll" %}
{% assign path = "/liquid" | prepend: baseurl %}
{{ path }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Apple : $20
/jekyll/liquid
{% endhighlight %}

**remove : 문자열에서 모든 특정 문구 제거하기**

remove 필터는 입력값 문자열에서 인자값으로 전달받은 문구(substring)를 모두 제거하는 필터이다. 입력값과 인자값에 String 타입이 아닌 값이 입력된 경우 String 타입으로 변환하여 작동한다.

{% highlight liquid %}
{% raw %}
{{ "What the fuck! This chicken is fucking delicious!" | remove: "ck" }}

{% assign string = "Iremove this sentenceloveremove this sentenceyouremove this sentence!" | remove: "remove this sentence" %}
{{ string }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
What the fu! This chien is fuing delicious!
Iloveyou!
{% endhighlight %}

**remove_first : 문자열에서 첫 번째 특정 문구 제거하기**

remove_first 필터는 입력값 문자열에서 인자값으로 전달받은 문구(substring) 중 처음 등장한 것만 제거하는 필터이다. 입력값과 인자값에 String 타입이 아닌 값이 입력된 경우 String 타입으로 변환하여 작동한다.

{% highlight liquid %}
{% raw %}
{{ "What the fuck! This chicken is fucking delicious!" | remove_first: "ck" }}

{% assign string = "Iremove this sentenceloveremove this sentenceyouremove this sentence!" | remove_first: "remove this sentence" %}
{{ string }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
What the fu! This chicken is fucking delicious!
Iloveremove this sentenceyouremove this sentence!
{% endhighlight %}

**replace : 문자열에서 모든 특정 문구 교체하기**

replace 필터는 입력값 문자열에서 첫 번째 인자값으로 전달받은 문구(substring)를 두 번째 인자값으로 모두 교체하는 필터이다. 입력값과 인자값에 String 타입이 아닌 값이 입력된 경우 String 타입으로 변환하여 작동한다.

{% highlight liquid %}
{% raw %}
{{ "What the fuck! This chicken is fucking delicious!" | replace: "fuck", "fuxx" }}

{% assign string = "John has 5 apples. John has 6 bananas." | replace: "John", "James" %}
{{ string }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
What the fuxx! This chicken is fuxxing delicious!
James has 5 apples. James has 6 bananas.
{% endhighlight %}

**replace_first : 문자열에서 첫 번째 특정 문구 교체하기**

replace_first 필터는 입력값 문자열에서 첫 번째 인자값으로 전달받은 문구(substring) 중 처음 등장한 것만 두 번째 인자값으로 교체하는 필터이다. 입력값과 인자값에 String 타입이 아닌 값이 입력된 경우 String 타입으로 변환하여 작동한다.

{% highlight liquid %}
{% raw %}
{{ "What the fuck! This chicken is fucking delicious!" | replace_first: "fuck", "fuxx" }}

{% assign string = "John has 5 apples. John has 6 bananas." | replace_first: "John", "James" %}
{{ string }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
What the fuxx! This chicken is fucking delicious!
James has 5 apples. John has 6 bananas.
{% endhighlight %}

**reverse : 배열 뒤집기**

reverse 필터는 입력값 배열의 순서를 뒤집는 필터이다. 만약 입력값이 Array 타입이 아니라면 해당 값이 있는 크기 1짜리 Array 타입으로 간주하고 필터가 작동한다. 이 경우 배열의 크기가 1이므로 필터가 적용돼도 출력은 동일하다.

{% highlight liquid %}
{% raw %}
{% assign array = "Apple,Banana,Tomato" | split: "," %}
{% for item in array %}
  - {{ item }}
{% endfor %}

{% assign array = array | reverse %}
{% for item in array %}
  - {{ item }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
- Apple
- Banana
- Tomato

- Tomato
- Banana
- Apple
{% endhighlight %}

참고로 reverse 필터는 문자열을 뒤집을 수는 없다. 만약 문자열을 뒤집고 싶다면 아래와 같이 split 필터를 이용해 문자열을 배열로 바꾼 후, 이를 reverse 필터로 뒤집고, 다시 join 필터로 문자열을 합치는 방법을 사용해야 한다.

{% highlight liquid %}
{% raw %}
{% assign string = "I love you!" %}
{% assign reversed_string = string | split: "" | reverse | join: "" %}

{{ string }}
{{ reversed_string }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
I love you!
!uoy evol I
{% endhighlight %}

**round : 반올림**

round 필터는 입력값을 반올림연산하는 필터이다. round 필터는 인자를 0개 또는 1개 받을 수 있는데, 0개인 경우(인자가 없다면) 가장 가까운 정수로 반올림하고, 1개인 경우 해당 소수점 자리까지 반올림한다. 만약 입력값과 인자가 Number가 아니라면 최대한 Number로 변환하여 해석하려 한다. 변환에 실패하면 0으로 간주한다.

{% highlight liquid %}
{% raw %}
{{ 1.2 | round }}
{{ -2.7 | round }}
{{ 3.0 | round }}

{% assign x = "123.987" | round : 2 %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
1
-3
3

123.99
{% endhighlight %}

**rstrip : 오른쪽 공백 제거**

rstrip 필터는 입력값의 오른쪽 모든 공백(Whitespace)[^17]을 제거하는 필터이다. 공백 문자가 아닌 글자 사이에 있는 (정상적인) 공백은 제거되지 않는다.

{% highlight liquid %}
{% raw %}
//////{{ "Hello     World!                 " | rstrip }}//////

{% assign x = "                 Hello     World!        " | rstrip %}
//////{{ x }}//////
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
//////Hello     World!//////
//////                 Hello     World!//////
{% endhighlight %}

**size : 크기 구하기**

size 필터는 입력값이 String 타입인 경우 문자열의 길이를 출력한다. 그리고 입력값이 Array 타입인 경우 배열의 크기(배열의 원소의 수)를 출력한다. 입력값이 Number 타입이거나 Boolean, Nil 타입이어도 문법 오류는 아니지만 이상하게 동작한다.[^19]

[^19]: Number 타입인 경우 항상 8을 출력한다. Boolean, Nil 타입인 경우 항상 0을 출력한다.

변수를 출력하는 경우 `|` 기호 말고도 `.`을 이용해 사용할 수도 있다.[^20]

[^20]: 상수를 출력할 때는 `.` 기호를 사용할 수 없다.

{% highlight liquid %}
{% raw %}
{{ "I love you!" | size }}

{% assign array = "Apple,Banana,Tomato" | split: "," %}
{{ array | size }}
{{ array.size }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
11
3
{% endhighlight %}

**slice : 문자열 자르기**

slice 필터는 입력값 String의 부분 문자열(substring)을 출력하는 필터이다. slice 필터는 두 개의 인자를 받을 수 있는데, 첫 번째 인자는 시작 인덱스[^21], 두 번째 인자는 길이를 의미한다. 예를 들어 `slice: 3, 5`라 하면 입력값 문자열의 인덱스 3부터 (인덱스 7까지) 길이 5의 부분 문자열을 추출하게 된다.

[^21]: 0부터 시작한다.

두 번째 인자의 경우 생략할 수 있다. 두 번째 인자를 생략한 경우 길이 1짜리 문자열(즉, 첫 번째 인자로 받은 인덱스에 해당하는 문자 하나)을 출력한다.

첫 번째 인자에 음수값을 사용할 수도 있는데, 이 경우 인덱스는 뒤에서부터 카운트된다.[^22]

[^22]: 문자열이 뒤집히지는 않는다.

{% highlight liquid %}
{% raw %}
{{ "pneumonoultramicroscopicsilicovolcanoconiosis" | slice: 0 }}
{{ "pneumonoultramicroscopicsilicovolcanoconiosis" | slice: 3 }}
{{ "pneumonoultramicroscopicsilicovolcanoconiosis" | slice: -2 }}
{{ "pneumonoultramicroscopicsilicovolcanoconiosis" | slice: 3, 15 }}

{% assign string = "pneumonoultramicroscopicsilicovolcanoconiosis" | slice: -10, 7 %}
{{ string }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
p
u
i
umonoultramicro

noconio
{% endhighlight %}

**sort : 배열 정렬하기 (대소문자 구별함)**

sort 필터는 입력값 배열의 원소를 정렬하는 필터이다. sort 필터는 인자를 0개 또는 1개 가질 수 있다. 인자가 없는 경우 알파벳 순으로 정렬한다.

{% highlight liquid %}
{% raw %}
{% assign array = "Tomato,Apple,avocado,Banana" | split: "," | sort %}
{% for item in array %}
  - {{ item }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
- Apple
- Banana
- Tomato
- avocado
{% endhighlight %}

인자가 주어진 경우 배열의 원소에서 인자값에 해당하는 속성으로 정렬한다. 예를 들어, 만약 블로그의 모든 컬렉션들이 순서를 나타내는 `order` 속성을 가지고 있다고 할 때, 컬렉션들을 `order` 순으로 정렬하려면 다음과 같이 하면 된다. 참고로 `site.collections`은 모든 컬렉션들의 배열이다.

{% highlight liquid %}
{% raw %}
{% assign collections = site.collections | sort: "order" %}
{% for item in collections %}
  - {{ item.name }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
- 미적분학 (Calculus)
- 기타 (Etc)
- Git
- Javascript
- 지킬 (Jekyll)
- 기계학습 (Machine Learning)
- NAS
- Numpy
- Re : 제로부터 배우는 파이썬
- Oracle VM VirtualBox
- 웹 서버 (Web Server)
{% endhighlight %}

참고로 역순으로 정렬하고 싶을 때는 [reverse 필터](#kramdown_reverse--배열-뒤집기)를 이용하면 된다.

**sort_natural : 배열 정렬하기 (대소문자 구별 안함)**

sort_natural 필터는 입력값 배열의 원소를 정렬하는 필터이다. [sort 필터](#kramdown_sort--배열-정렬하기-대소문자-구별함)와의 차이점은 sort 필터의 경우 대소문자를 구별하지만[^23], sort_natural 필터는 구별하지 않는다는 것이다.[^24] 나머지는 모두 sort 필터와 동일하다.

[^23]: 대문자는 소문자보다 정렬 순서가 빠르다. 즉, "A"가 "a"보다 앞에 위치한다.
[^24]: "A"와 "a"는 정렬 순서가 동일하다. 또한 "a"가 "B"가 보다 앞에 위치한다.

{% highlight liquid %}
{% raw %}
{% assign array = "Tomato,Apple,avocado,Banana" | split: "," | sort_natural %}
{% for item in array %}
  - {{ item }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
- Apple
- avocado
- Banana
- Tomato
{% endhighlight %}

**split : 문자열로부터 배열 만들기**

split 필터는 입력값 문자열로부터 배열을 만드는 필터이다. split 필터는 인자로 문자열을 하나 받는데, 이 인자값을 기준으로 입력값 문자열을 나눠 각각을 배열의 원소로 만든다.

split 필터를 이용해 배열을 만드는 방법은 명시적으로 배열을 선언할 수 없는 Liquid에서 배열을 선언하는 사실상 표준으로 사용된다.

{% highlight liquid %}
{% raw %}
{% assign array = "Apple,Banana,Tomato" | split: "," %}
{% for item in array %}
  - {{ item }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
- Apple
- Banana
- Tomato
{% endhighlight %}

**strip : 좌우 공백 제거**

strip 필터는 입력값의 좌우 모든 공백(Whitespace)[^17]을 제거하는 필터이다. 공백 문자가 아닌 글자 사이에 있는 (정상적인) 공백은 제거되지 않는다. [lstrip 필터](#kramdown_lstrip--왼쪽-공백-제거)와 [rstrip 필터](#kramdown_rstrip--오른쪽-공백-제거)를 합한 필터이다.

{% highlight liquid %}
{% raw %}
//////{{ "Hello     World!" | strip }}//////

{% assign x = "                 Hello     World!        " | strip %}
//////{{ x }}//////
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
//////Hello     World!//////
//////Hello     World!//////
{% endhighlight %}

**strip_html : HTML 태그 제거**

strip_html 필터는 입력값 문자열에서 모든 HTML 태그를 제거하는 필터이다.

{% highlight liquid %}
{% raw %}
{{ "This is <bold>very</bold> important!" | strip_html }}

{% assign stripped_html = '<p>I <a href="https://en.wikipedia.org/wiki/Love">love</a> you <em>SO MUCH</em>!</p>' | strip_html %}
{{ stripped_html }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
This is very important!
I love you SO MUCH!
{% endhighlight %}

**strip_newlines : 개행 문자 제거**

strip_newlines 필터는 입력값 문자열에서 개행 문자(`\n`)를 제거하는 필터이다.

{% highlight liquid %}
{% raw %}
{% capture string %}
Hello
World!
{% endcapture %}

{{ string | strip_newlines }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
HelloWorld!
{% endhighlight %}

**times : 곱셈**

times 필터는 입력값에 인자값을 곱하는 필터이다. 입력값과 인자값에는 Number 타입의 값을 사용해야 한다. 만약 Number 타입이 아닌 값이 사용되면 최대한 Number로 해석하려 하고, 실패하면 0으로 간주한다.

{% highlight liquid %}
{% raw %}
{{ 16 | times: 4 }}

{% assign x = -5.5 | times: 20 %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
64
-110.0
{% endhighlight %}

**truncate : 문자열 축약**

truncate 필터는 입력값 문자열을 축약하는 필터이다. truncate 필터는 인자를 2개 받을 수 있다. 첫 번째 인자는 필수로, 입력값의 문자열을 몇 글자까지 남길지를 결정한다. 만약 입력값 문자열의 길이가 첫 번째 인자값보다 작을 경우 아무 일도 일어나지 않는다. 두 번째 인자는 입력값 문자열이 축약될 때 마지막에 축약되었음을 나타낼 문자열을 결정한다. 두 번째 인자는 생략할 경우 생략 부호(ellipsis, "...")가 디폴트로 들어간다.

주의해야 할 것은 두 번째 인자로 주어진 문자열의 길이도 첫 번째 인자로 주어지는 남길 글자의 수에 영향을 끼친다는 것이다. 예를 들어, 첫 번째 인자로 20을 주고 두 번째 인자로 ", and so on"(11글자)을 사용한다면, 입력값 문자열에서는 앞 9글자만 남고 두 번째 인자 ", and so on"이 뒤에 붙어 도합 20글자가 되는 것이다. 두 번째 인자에 아무 값을 사용하지 않으면 디폴트로 "..."(3글자)가 들어간다는 점에 유의하자. 만약 두 번째 인자에 아무 값을 사용하지 않은 상태에서 입력값 문자열에서 20글자를 정확히 남기고 싶다면 첫 번째 인자로 23을 입력해야 한다.

{% highlight liquid %}
{% raw %}
{{ "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ligula nunc, sollicitudin in lacus eget, ultricies porta neque. Mauris viverra lobortis ipsum ut facilisis. Nulla arcu arcu, malesuada sed sollicitudin eget, luctus quis orci." | truncate: 20 }}

{{ "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ligula nunc, sollicitudin in lacus eget, ultricies porta neque. Mauris viverra lobortis ipsum ut facilisis. Nulla arcu arcu, malesuada sed sollicitudin eget, luctus quis orci." | truncate: 20, ", blah blah blah." }}

{% assign string = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ligula nunc, sollicitudin in lacus eget, ultricies porta neque. Mauris viverra lobortis ipsum ut facilisis. Nulla arcu arcu, malesuada sed sollicitudin eget, luctus quis orci." | truncate: 20, "" %}
{{ string }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Lorem ipsum dolor...
Lor, blah blah blah.
Lorem ipsum dolor si
{% endhighlight %}

**truncatewords : 문자열 축약 (단어 단위)**

truncatewords 필터는 입력값 문자열을 축약하는 필터이다. [truncate 필터](#kramdown_truncate--문자열-축약)와의 차이점은, truncate 필터는 글자 수 단위로 축약하지만, truncatewords 필터는 단어 단위로 축약한다는 것이다.

truncatewords 필터 역시 인자를 2개 받을 수 있다. 첫 번째 인자는 필수로, 입력값의 문자열에서 몇 개의 단어까지 남길지를 결정한다. 만약 입력값 문자열의 단어 개수가 첫 번째 인자값보다 작을 경우 아무 일도 일어나지 않는다. 두 번째 인자는 입력값 문자열이 축약될 때 마지막에 축약되었음을 나타낼 문자열을 결정한다. 두 번째 인자는 생략할 경우 생략 부호(ellipsis, "...")가 디폴트로 들어간다.

{% highlight liquid %}
{% raw %}
{{ "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ligula nunc, sollicitudin in lacus eget, ultricies porta neque. Mauris viverra lobortis ipsum ut facilisis. Nulla arcu arcu, malesuada sed sollicitudin eget, luctus quis orci." | truncatewords: 3 }}

{{ "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ligula nunc, sollicitudin in lacus eget, ultricies porta neque. Mauris viverra lobortis ipsum ut facilisis. Nulla arcu arcu, malesuada sed sollicitudin eget, luctus quis orci." | truncatewords: 3, ", blah blah blah." }}

{% assign string = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ligula nunc, sollicitudin in lacus eget, ultricies porta neque. Mauris viverra lobortis ipsum ut facilisis. Nulla arcu arcu, malesuada sed sollicitudin eget, luctus quis orci." | truncatewords: 3, "" %}
{{ string }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
Lorem ipsum dolor...
Lorem ipsum dolor, blah blah blah.
Lorem ipsum dolor
{% endhighlight %}

**uniq : 배열 중복 원소 제거**

uniq 필터는 입력값 배열에서 중복 요소를 제거하는 필터이다. 만약 입력값이 Array 타입이 아니라면 해당 값이 있는 크기 1짜리 Array 타입으로 간주하고 필터가 작동한다. 이 경우 배열의 크기가 1이므로 필터가 적용돼도 출력은 동일하다.

{% highlight liquid %}
{% raw %}
{% assign array = "Apple,Banana,Apple,Tomato,Apple" | split: "," | uniq %}
{% for item in array %}
  - {{ item }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
- Apple
- Banana
- Tomato
{% endhighlight %}

**upcase : 대문자로**

upcase 필터는 입력값을 대문자로 바꾸는 필터이다. 만약 입력값이 String이 아니라면 String으로 자동 변환되어 처리된다.

{% highlight liquid %}
{% raw %}
{{ "hello world!" | upcase }}

{% assign x = "hElLo WoRlD!" | upcase %}
{{ x }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
HELLO WORLD!
HELLO WORLD!
{% endhighlight %}

**url_decode : URL 디코딩**

url_decode 필터는 입력값 문자열에서 URL 인코딩을 해제하는(디코딩하는) 필터이다.

{% highlight liquid %}
{% raw %}
{{ "url %EB%94%94%EC%BD%94%EB%94%A9" | url_decode }}

{% assign decoded_email = "park.heekang33%40gmail.com" | url_decode %}
{{ decoded_email }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
url 디코딩
park.heekang33@gmail.com
{% endhighlight %}

**url_encode : URL 인코딩**

url_encode 필터는 입력값 문자열에서 URL-safe하지 않은 문자들을 URL-safe하게 인코딩하는 필터이다.

{% highlight liquid %}
{% raw %}
{{ "url 인코딩" | url_encode }}

{% assign encoded_email = "park.heekang33@gmail.com" | url_encode %}
{{ encoded_email }}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
url+%EC%9D%B8%EC%BD%94%EB%94%A9
park.heekang33%40gmail.com
{% endhighlight %}

**where : 배열로부터 새로운 배열 추출하기 (값)**

where 필터는 입력값 배열의 요소들 중 첫 번째 인자로 전달받은 속성의 값이 두 번째 인자로 전달받은 값과 같은 요소만 추출하여 새로운 배열을 만드는 필터이다.

예를 들어, 블로그 전체 컬렉션들의 배열 `site.collections`에서 `output` 속성이 true인 컬렉션만을 추출해 새로운 배열을 만드려면 다음과 같이 하면 된다.

{% highlight liquid %}
{% raw %}
{% assign all_collections = site.collections %}
{% for collection in all_collections %}
  - {{ collection.name }}
{% endfor %}

{% assign selected_collections = all_collections | where: "output", true %}
{% for collection in selected_collections %}
  - {{ collection.name }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
- 미적분학 (Calculus)
- 기타 (Etc)
- Git
- Javascript
- 지킬 (Jekyll)
- 기계학습 (Machine Learning)
- NAS
- Numpy
- Re : 제로부터 배우는 파이썬
- Oracle VM VirtualBox
- 웹 서버 (Web Server)

- 미적분학 (Calculus)
- Javascript
- 지킬 (Jekyll)
- 기계학습 (Machine Learning)
- Numpy
- Re : 제로부터 배우는 파이썬
{% endhighlight %}

Liquid에서는 배열을 원하는 대로 초기화할 수 없고, 하위 속성을 마음대로 추가/삭제할 수 없다. 그래서 필자의 경우 where 필터를 잘 사용하지 않는다.

**where_exp : 배열로부터 새로운 배열 추출하기 (조건식)**

where_exp 필터는 입력값 배열의 요소들 중 두 번째 인자로 전달받은 조건식을 만족시키는 요소만 추출하여 새로운 배열을 만드는 필터이다. 첫 번째 요소는 배열의 각 요소를 순회할 때 쓰는 임시 변수 역할을 한다. 모든 where 필터는 where_exp 필터로 바꿀 수 있지만 그 역은 성립하지 않는다.

예를 들어 특정 컬렉션 `collection`이 있을 때, 이 컬렉션 안의 모든 문서들의 배열 `collection.docs`에서 문서의 순서를 나타내는 `order` 속성이 설정된 문서만을 뽑는 경우를 생각해 보자(참고로 `order` 속성은 필자가 임의로 만든 것이다). 그런데 where 필터는 특정 속성이 특정 "값"을 가진 요소만 추출하는 필터이다. `order` 속성의 경우 문서마다 값이 다를 것이므로(첫 번째 문서는 `order: 1`, 두 번째 문서는 `order: 2`와 같이 되어 있을 것이다) 이 경우 where 필터를 사용할 수 없다. 하지만 where_exp 필터는 값이 아닌 조건식을 받기에 다음과 같이 하면 된다.

{% highlight liquid %}
{% raw %}
{% for doc in collection %}
  - {{ doc.title }}
{% endfor %}

{% assign selected_docs = collection | where_exp: "item", "item.order" %}
{% for doc in selected_docs %}
  - {{ doc.title }}
{% endfor %}
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text %}
- 서론
- 지킬(Jekyll) 설치하기
- _config.yml
- 지킬 디렉토리 구조
- 지킬 렌더링 순서
- Liquid

- 서론
- 지킬(Jekyll) 설치하기
- _config.yml
- Liquid
{% endhighlight %}

이 필터는 지킬 Liquid에서만 지원하는 필터이다.

# 4. 공백 처리

Liquid는 Liquid 문법 요소**만** 바꾸고, 나머지는 건드리지 않는다.

{% highlight liquid linenos %}
{% raw %}
<div>
  {% assign true_statement = "Good! :-)" %}
  {% assign false_statement = "Bad! :-(" %}

  {% assign condition = true %}

  {% if condition %}
    {{ true_statement }}
  {% else %}
    {{ false_statement }}
  {% endif %}
</div>
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text linenos %}
<div>
  {% assign true_statement = "Good! :-)" %}
  {% assign false_statement = "Bad! :-(" %}

  {% assign condition = true %}

  {% if condition %}
    {{ true_statement }}
  {% else %}
    {{ false_statement }}
  {% endif %}
</div>
{% endhighlight %}

위 코드에서 2번째 줄의 Liquid 구문 `{% raw %}{% assign true_statement = "Good! :-)" %}{% endraw %}`은 렌더링될 때 아무 값도 출력하지 않고 그대로 사라지지만, Liquid 코드 앞의 띄어쓰기와 코드 뒤의 개행 문자는 그대로 남는다. 이런 식으로 나머지 줄에서도 공백 문자는 모두 남아 [실행 결과]와 같이 공백이 많이 남게 된다. 다행히 &lt;div&gt;를 비롯한 대부분의 HTML 태그는 앞뒤 공백 문자를 무시하므로 대부분의 경우 이 현상은 큰 문제가 되지 않는다.

하지만 공백이 반드시 없어야 하는 경우가 있다. 이 경우 `-` 기호를 사용하여 `{% raw %}{{- ... -}}{% endraw %}`, `{% raw %}{%- ... -%}{% endraw %}`라 입력하면 렌더링 시 좌우의 모든 공백 문자를 제거한다.

{% highlight liquid linenos %}
{% raw %}
<div>
  {%- assign true_statement = "Good! :-)" -%}
  {%- assign false_statement = "Bad! :-(" -%}

  {%- assign condition = true -%}

  {%- if condition -%}
    {{- true_statement -}}
  {%- else -%}
    {{- false_statement -}}
  {%- endif -%}
</div>
{% endraw %}
{% endhighlight %}

{: .code-result}
{% highlight text linenos %}
<div>
  {%- assign true_statement = "Good! :-)" -%}
  {%- assign false_statement = "Bad! :-(" -%}

  {%- assign condition = true -%}

  {%- if condition -%}
    {{- true_statement -}}
  {%- else -%}
    {{- false_statement -}}
  {%- endif -%}
</div>
{% endhighlight %}

# 지킬과의 상호작용

## 지킬 변수

**예제: 목차 (TOC)**

Liquid는 분명 한계가 많은 템플릿 언어이지만, 잘 쓰면 아주 재미있는 기능들을 만들 수 있다.

예를 들어, 본 블로그에서 사용하고 있는 목차 기능은 순수 Liquid만을 이용해 만들어졌다. allejo의 [jekyll-toc](https://github.com/allejo/jekyll-toc)의 코드를 참조하여 직접 만들었다.

{% highlight html %}
{% raw %}
{% assign h1counter = 0 %}
{% assign h2counter = 0 %}
{% assign h3counter = 0 %}
{% assign h4counter = 0 %}
{% assign h5counter = 0 %}
{% assign h6counter = 0 %}

{% assign nodes = include.html | split: "<h" %}

<div class="toc{% if nodes.size == 1 %} hidden {% endif %}">
    <p class="toc-title">목차</p>

    <div class="toc-content">
    {% for node in nodes %}
        {% if node == "" %}
            {% continue %}
        {% endif %}

        {% assign headerLevel = node | replace: '"', '' | slice: 0, 1 | times: 1 %}

        {% comment %}
        {% if headerLevel == 0 %}
            {% continue %}
        {% endif %}
        {% endcomment %}

        {% assign _temp = node | split: "</h" %}
        {% assign _temp = _temp[0] | split: ">" %}
        {% assign headerContent = _temp[1] | strip %}

        {% assign _temp = node | split: "</h" %}
        {% assign _temp = _temp[0] | split: 'id="' %}
        {% assign _temp = _temp[1] | split: '"' %}
        {% assign headerID = _temp[0] | strip %}

        {% case headerLevel %}
            {% when 0 %}
                {% continue %}
            {% when 1 %}
                {% assign h1counter = h1counter | plus: 1 %}
                {% assign h2counter = 0 %}
                {% assign h3counter = 0 %}
                {% assign h4counter = 0 %}
                {% assign h5counter = 0 %}
                {% assign h6counter = 0 %}
                <p class="toc-item toc-{{ headerLevel }}" id="toc-{{ headerID }}"><a href="#{{ headerID }}">{{ h1counter }}.</a> {{ headerContent }}</p>
            {% when 2 %}
                {% assign h2counter = h2counter | plus: 1 %}
                {% assign h3counter = 0 %}
                {% assign h4counter = 0 %}
                {% assign h5counter = 0 %}
                {% assign h6counter = 0 %}
                <p class="toc-item toc-{{ headerLevel }}" id="toc-{{ headerID }}"><a href="#{{ headerID }}">{{ h1counter }}.{{ h2counter }}.</a> {{ headerContent }}</p>
            {% when 3 %}
                {% assign h3counter = h3counter | plus: 1 %}
                {% assign h4counter = 0 %}
                {% assign h5counter = 0 %}
                {% assign h6counter = 0 %}
                <p class="toc-item toc-{{ headerLevel }}" id="toc-{{ headerID }}"><a href="#{{ headerID }}">{{ h1counter }}.{{ h2counter }}.{{ h3counter }}.</a> {{ headerContent }}</p>
            {% when 4 %}
                {% assign h4counter = h4counter | plus: 1 %}
                {% assign h5counter = 0 %}
                {% assign h6counter = 0 %}
                <p class="toc-item toc-{{ headerLevel }}" id="toc-{{ headerID }}"><a href="#{{ headerID }}">{{ h1counter }}.{{ h2counter }}.{{ h3counter }}.{{ h4counter }}.</a> {{ headerContent }}</p>
            {% when 5 %}
                {% assign h5counter = h5counter | plus: 1 %}
                {% assign h6counter = 0 %}
                <p class="toc-item toc-{{ headerLevel }}" id="toc-{{ headerID }}"><a href="#{{ headerID }}">{{ h1counter }}.{{ h2counter }}.{{ h3counter }}.{{ h4counter }}.{{ h5counter }}.</a> {{ headerContent }}</p>
            {% when 6 %}
                {% assign h6counter = h6counter | plus: 1 %}
                <p class="toc-item toc-{{ headerLevel }}" id="toc-{{ headerID }}"><a href="#{{ headerID }}">{{ h1counter }}.{{ h2counter }}.{{ h3counter }}.{{ h4counter }}.{{ h5counter }}.{{ h6counter }}</a> {{ headerContent }}</p>
        {% endcase %}    
    {% endfor %}
    </div>
</div>
{% endraw %}
{% endhighlight %}
