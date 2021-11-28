# HTML Cheatsheet

> HTML 치트시트입니다.



## Table of Contents
****
- [HTML Cheatsheet](#html-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [HTML 보일러플레이트](#html-보일러플레이트)
    - [`<!DOCTYPE html>`](#doctype-html)
    - [`<html lang="en"></html>`](#html-langenhtml)
    - [`<head></head>`](#headhead)
    - [`<meta charset="UTF-8">`](#meta-charsetutf-8)
    - [`<meta http-equiv="X-UA-Compatible" content="IE=edge">`](#meta-http-equivx-ua-compatible-contentieedge)
    - [`<meta name="viewport" content="width=device-width, initial-scale=1.0">`](#meta-nameviewport-contentwidthdevice-width-initial-scale10)
    - [`<title>Document</title>`](#titledocumenttitle)
    - [`<body></body>`](#bodybody)
    - [`파비콘(favicon)`](#파비콘favicon)
    - [`CSS Reset`](#css-reset)
    - [`Custom Style Sheet`](#custom-style-sheet)
    - [참고자료](#참고자료)
  - [시맨틱 태그](#시맨틱-태그)
    - [참고자료](#참고자료-1)
  - [많이 사용되는 태그](#많이-사용되는-태그)
  - [메타 태그 & OG](#메타-태그--og)
    - [메타 태그](#메타-태그)
      - [태그 1](#태그-1)
      - [태그 2](#태그-2)
    - [OG(Open Graph)](#ogopen-graph)
  - [폼](#폼)
  - [엔티티](#엔티티)
  - [이미지 & 미디어](#이미지--미디어)


<br>

---

<br>


## HTML 보일러플레이트
> HTML 작성 시 재사용할 수 있는 [보일러플레이트(Boilerplate) 코드](https://ko.wikipedia.org/wiki/%EC%83%81%EC%9A%A9%EA%B5%AC_%EC%BD%94%EB%93%9C)입니다.


```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Favicon -->
  <link rel="icon" href="favicon.ico" type="image/x-icon">
  <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
  <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">
  <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png">
  <link rel="manifest" href="/site.webmanifest">
  <link rel="mask-icon" href="/safari-pinned-tab.svg" color="#5bbad5">
  <meta name="msapplication-TileColor" content="#da532c">
  <meta name="theme-color" content="#ffffff">

  <!-- CSS Reset -->
  <link rel="stylesheet" href="css/normalize.css" />

  <!-- Custom Style Sheet -->
  <link rel="stylesheet" href="css/main.css" />

  <title>Document</title>
</head>
<body>
  
</body>
</html>
```
### `<!DOCTYPE html>`
- 문서의 형식을 정의한다. 브라우저에게 현재 문서가 HTML 언어로 작성된 문서임을 알린다.

<br>

### `<html lang="en"></html>`
- HTML 문서의 루트를 나타내는 최상위 엘리먼트다. `lang` 속성을 통해 문서의 언어를 설정한다.
  1. 웹 접근성 도움: 화면 낭독기의 언어 선택에 도움을 줌
  2. 검색 엔진 최적화 향상: 검색 결과 품질 높임
  3. 컨텐츠 스타일 설정 도움: 언어별 컨텐츠 스타일 적절히 변경(글꼴 등)

<br>

### `<head></head>`
  - 사용자 눈에 직접적으로 보이지 않는 문서의 [메타 데이터](https://ko.wikipedia.org/wiki/%EB%A9%94%ED%83%80%EB%8D%B0%EC%9D%B4%ED%84%B0)를 정의한다.

<br>

### `<meta charset="UTF-8">` 
- HTML 문자 인코딩 방식을 정의한다.  `UTF-8` 유니코드 방식은 세계 거의 모든 문자와 기호를 표현할 수 있다.

<br>

### `<meta http-equiv="X-UA-Compatible" content="IE=edge">`
- 브라우저 호환성을 설정한다. 인터넷 익스플로러가 최신 버전으로 마크업을 해석하게끔 한다.
- [레거시 브라우저를 지원해야하는 상황이 아니라면 완전히 제거하는 것을 권장한다.](https://stackoverflow.com/questions/6771258/what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do)

<br>

### `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
- 페이지가 다양한 디바이스들에서 잘 표현될 수 있도록 한다. 페이지 너비와 줌 레벨을 제어한다.

<br>

### `<title>Document</title>`
- 페이지의 제목을 정의하며, 아래 항목에 활용된다.
  1. 브라우저 제목 표시줄
  2. 북마크 및 즐겨찾기
  3. 검색 서비스의 검색 결과 목록

<br>

### `<body></body>`
- 사용자에게 보여줄 웹 페이지의 컨텐츠를 정의한다.

<br>

### `파비콘(favicon)`
- 브라우저 탭에 보이는 페이지를 나타내는 아이콘을 의미한다.
- 최근에는 여러 형태의 아이콘(touch, tile 등)이 등장하여 혼란스러운 면이 있는데, [RealFaviconGenerator](https://realfavicongenerator.net/), [Favicon-Generator](https://www.favicon-generator.org/)와 같은 파비콘 자동 생성 서비스를 사용하면 편리하다.

<br>

### `CSS Reset`
- 브라우저 마다 각기 다른 기본 스타일을 "재설정(Reset)"하여 페이지의 일관된 스타일을 보장한다.
- [Meyer's CSS Reset](https://meyerweb.com/eric/tools/css/reset/)
  - 거의 모든 요소의 기본 스타일을 제거하여 균일한 시각적 스타일을 가지게끔 만든다.
- [normailize.css](https://github.com/necolas/normalize.css)
  - 유용한 기본 브라우저 스타일을 유지한다. 즉, 일반적인 요소의 스타일을 재선언할 필요가 없다.
- (참고) [ress](https://github.com/filipelinhares/ress)
  - 위 두 방식의 장점을 취하는 것을 목표로 한다.

<br>

### `Custom Style Sheet`
- css 파일을 분리하여 모든 스타일 관련 지침을 작성한다.
- [구글 스타일 가이드 3.1.5](https://google.github.io/styleguide/htmlcssguide.html#Separation_of_Concerns)에 따르면 웹 페이지의 **구조와 콘텐츠**를 **스타일**과 **분리**하도록 권장하고 있다.

<br>

### 참고자료
- [HTML5 ★ BOILERPLATE](https://html5boilerplate.com/)
- [Boilerplate HTML code](https://medium.com/web-dev-survey-from-kyoto/boilerplate-html-code-60229f38d0d4)
- [Basic HTML5 Template: Use This HTML Boilerplate as a Starter for Any Web Dev Project](https://www.freecodecamp.org/news/basic-html5-template-boilerplate-code-example/)
- [Understanding the Tags in HTML Boilerpate](https://betterprogramming.pub/understanding-the-tags-in-html-boilerplate-38d1ae2805f7)
- [HTML/CSS Lang 프로퍼티 및 어트리뷰트 방법 및 예제](https://webisfree.com/2019-02-27/html-css-lang-%ED%94%84%EB%A1%9C%ED%8D%BC%ED%8B%B0-%EB%B0%8F-%EC%96%B4%ED%8A%B8%EB%A6%AC%EB%B7%B0%ED%8A%B8-%EB%B0%A9%EB%B2%95-%EB%B0%8F-%EC%98%88%EC%A0%9C)
- [About normailize.css](https://nicolasgallagher.com/about-normalize-css/)

<br>

[🔝 BACK TO TOP](#Table-of-Contents)


---

<br>


## 시맨틱 태그

> 주제 설명

### 참고자료
- [Google에서 인식하는 모든 메타 태그](https://developers.google.com/search/docs/advanced/crawling/special-tags)
- [10 Most Important Meta Tags You Need to Know for SEO](https://www.searchenginejournal.com/important-tags-seo/156440/)
- [The Open Graph protocol](https://ogp.me/)

<br>

[🔝 BACK TO TOP](#Table-of-Contents)


---

<br>


## 많이 사용되는 태그

> 주제 설명


<br>

[🔝 BACK TO TOP](#Table-of-Contents)


---

<br>


## 메타 태그 & OG

### 메타 태그

> 메타 태그는 이런 것입니다.



#### 태그 1

- 태그1은 궁시렁 궁시렁 궁시렁입니다.
  ```html
  <meta>
  ```
  
  - [추가설명](./html/meta1.md)
  - [외부링크]()



#### 태그 2

- 태그2는 궁시렁 궁시렁입니다.


<br>

[🔝 BACK TO TOP](#Table-of-Contents)


---

<br>


### OG(Open Graph)

> OG는 Open Graph(오픈 그래프)의 약자로 이런 것입니다.


<br>

[🔝 BACK TO TOP](#Table-of-Contents)


---

<br>


## 폼

> 주제 설명


<br>

[🔝 BACK TO TOP](#Table-of-Contents)


---

<br>


## 엔티티

> 주제 설명


<br>

[🔝 BACK TO TOP](#Table-of-Contents)


---

<br>


## 이미지 & 미디어

> 주제 설명


<br>

[🔝 BACK TO TOP](#Table-of-Contents)


---

<br>