# HTML 치트시트

- [HTML 치트시트](#html-치트시트)
  - [HTML 보일러플레이트](#html-보일러플레이트)
    - [`파비콘(favicon)`](#파비콘favicon)
    - [`CSS Reset`](#css-reset)
    - [`Custom Style Sheet`](#custom-style-sheet)
  - [시맨틱 태그](#시맨틱-태그)
  - [많이 사용되는 태그](#많이-사용되는-태그)
  - [메타 태그](#메타-태그)
    - [`application-name`](#application-name)
    - [`description`](#description)
    - [`author`](#author)
    - [`generator`](#generator)
    - [`keywords`](#keywords)
    - [`referrer`](#referrer)
    - [`theme-color`](#theme-color)
    - [`color-scheme`](#color-scheme)
  - [OG(Open Graph)](#ogopen-graph)
    - [Basic Metadata](#basic-metadata)
    - [Optional Metadata](#optional-metadata)
  - [폼](#폼)
  - [엔티티](#엔티티)
  - [이미지 & 미디어](#이미지--미디어)
    - [이미지(`<img>`)](#이미지img)
    - [비디오(`<video>`)](#비디오video)
    - [오디오(`<audio>`)](#오디오audio)

<br>

---

<br>

## HTML 보일러플레이트
> HTML 작성 시 재사용할 수 있는 [보일러플레이트(Boilerplate) 코드](https://ko.wikipedia.org/wiki/%EC%83%81%EC%9A%A9%EA%B5%AC_%EC%BD%94%EB%93%9C)입니다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <!-- Favicon -->
    <link rel="icon" href="favicon.ico" type="image/x-icon" />
    <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png" />
    <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png" />
    <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png" />
    <link rel="manifest" href="/site.webmanifest" />
    <link rel="mask-icon" href="/safari-pinned-tab.svg" color="#5bbad5" />
    <meta name="msapplication-TileColor" content="#da532c" />
    <meta name="theme-color" content="#ffffff" />

    <!-- CSS Reset -->
    <link rel="stylesheet" href="css/normalize.css" />

    <!-- Custom Style Sheet -->
    <link rel="stylesheet" href="css/main.css" />

    <title>Document</title>
  </head>
  <body></body>
</html>
```

- `<!DOCTYPE html>`
  - 문서의 형식을 정의한다. 브라우저에게 현재 문서가 HTML 언어로 작성된 문서임을 알린다.
- `<html lang="en"></html>`
  - HTML 문서의 루트를 나타내는 최상위 엘리먼트다. `lang` 속성을 통해 문서의 언어를 설정한다.
    1. 웹 접근성 도움: 화면 낭독기의 언어 선택에 도움을 줌
    2. 검색 엔진 최적화 향상: 검색 결과 품질 높임
    3. 컨텐츠 스타일 설정 도움: 언어별 컨텐츠 스타일 적절히 변경(글꼴 등)
- `<head></head>`
  - 사용자 눈에 직접적으로 보이지 않는 문서의 [메타 데이터](https://ko.wikipedia.org/wiki/%EB%A9%94%ED%83%80%EB%8D%B0%EC%9D%B4%ED%84%B0)를 정의한다.
- `<meta charset="UTF-8">`
  - HTML 문자 인코딩 방식을 정의한다. `UTF-8` 유니코드 방식은 세계 거의 모든 문자와 기호를 표현할 수 있다.
- `<meta http-equiv="X-UA-Compatible" content="IE=edge">`
  - 브라우저 호환성을 설정한다. 인터넷 익스플로러가 최신 버전으로 마크업을 해석하게끔 한다.
  - [레거시 브라우저를 지원해야하는 상황이 아니라면 완전히 제거하는 것을 권장한다.](https://stackoverflow.com/questions/6771258/what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do)
- `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
  - 페이지가 다양한 디바이스들에서 잘 표현될 수 있도록 한다. 페이지 너비와 줌 레벨을 제어한다.
- `<title>Document</title>`
  - 페이지의 제목을 정의하며, 아래 항목에 활용된다.
    1. 브라우저 제목 표시줄
    2. 북마크 및 즐겨찾기
    3. 검색 서비스의 검색 결과 목록
- `<body></body>`
  - 사용자에게 보여줄 웹 페이지의 컨텐츠를 정의한다.

### `파비콘(favicon)`

- 브라우저 탭에 보이는 페이지를 나타내는 아이콘을 의미한다.
- 최근에는 여러 형태의 아이콘(touch, tile 등)이 등장하여 혼란스러운 면이 있는데, [RealFaviconGenerator](https://realfavicongenerator.net/), [Favicon-Generator](https://www.favicon-generator.org/)와 같은 파비콘 자동 생성 서비스를 사용하면 편리하다.

### `CSS Reset`

- 브라우저 마다 각기 다른 기본 스타일을 "재설정(Reset)"하여 페이지의 일관된 스타일을 보장한다.
- [Meyer's CSS Reset](https://meyerweb.com/eric/tools/css/reset/)
  - 거의 모든 요소의 기본 스타일을 제거하여 균일한 시각적 스타일을 가지게끔 만든다.
- [normailize.css](https://github.com/necolas/normalize.css)
  - 유용한 기본 브라우저 스타일을 유지한다. 즉, 일반적인 요소의 스타일을 재선언할 필요가 없다.
- (참고) [ress](https://github.com/filipelinhares/ress)
  - 위 두 방식의 장점을 취하는 것을 목표로 한다.

### `Custom Style Sheet`

- css 파일을 분리하여 모든 스타일 관련 지침을 작성한다.
- [구글 스타일 가이드 3.1.5](https://google.github.io/styleguide/htmlcssguide.html#Separation_of_Concerns)에 따르면 웹 페이지의 **구조와 콘텐츠**를 **스타일**과 **분리**하도록 권장하고 있다.

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

## 시맨틱 태그

> 주제 설명

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

## 메타 태그

> 웹 페이지에 대한 [메타데이터](https://ko.wikipedia.org/wiki/%EB%A9%94%ED%83%80%EB%8D%B0%EC%9D%B4%ED%84%B0)를 제공하기 위한 `<meta ...>` 형태의 태그를 말한다.

- `meta` 요소가 제공하는 메타 데이터의 4가지 유형
  1. `name` 속성
     - 문서의 메타 데이터를 설정한다.
     - `name` 속성과 `content` 속성이라는 이름-값 쌍 형태로 제공한다.
  2. `http-equiv` 속성
     - 프래그마 지시문(pragma directive)을 설정한다.
  3. `charset` 속성
     - 문자열 형식 정보를 제공한다.
  4. `itemporp` 속성
     - 사용자가 정의한 메타 데이터(`user-defined metadata`)

### `application-name`

- 웹 페이지에서 구동 중인 웹 애플리케이션의 이름
- 종종 `<title>` 태그에 애플리케이션 이름이 아닌 특정 페이지의 이름 또는 상태 정보가 존재할 수 있기 때문에, 사용자 에이전트는 `<title>`이 아닌 `application-name`을 사용할 수 있다.

  ```html
  <!-- 정확한 애플리케이션 이름을 나타낸다. -->
  <meta name="application-name" content="예쁜템들 모여사는 오늘의집" />

  <!-- 상세 페이지에 들어가면 애플리케이션 이름이 아닌 다른 데이터를 함께 표시하는 경우가 있다. -->
  <title>
    인기 인테리어 집들이 모음ㅣ예쁜템들 모여사는 오늘의집 유저들의 집꾸미기
  </title>
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### `description`

- 페이지에 대한 짧고 명확한 요약
  ```html
  <meta
    name="description"
    content="2000만이 선택한 No.1 인테리어 필수앱. 집들이 구경부터 제품 정보 확인, 구매까지 한 번에!"
  />
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### `author`

- 문서 저작자

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### `generator`

- 문서를 생성하는 데 사용된 소프트웨어 패키지
  ```html
  <meta name="generator" content="Frontweaver 8.2" />
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### `keywords`

- 페이지의 콘텐츠와 관련된 쉼표(`,`)로 구분한 키워드 목록
  ```html
  <meta
    name="keywords"
    content="만화, 웹툰, 무료, 성인, BL, 추천, 요일별, 코믹스, 카툰, 사이트"
  />
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### `referrer`

- 문서에 대한 [HTTP Referer](https://ko.wikipedia.org/wiki/HTTP_%EB%A6%AC%ED%8D%BC%EB%9F%AC) 관련 정책
  ```html
  <meta name="referrer" content="no-referrer-when-downgrade" />
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### `theme-color`

- 유저 에이전트가 페이지 또는 주변 사용자 인터페이스의 표시를 커스터마이징하는 데 사용할 색상
  ```html
  <meta name="theme-color" content="#3c790a" />
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### `color-scheme`

- 유저 에이전트가 페이지 배경을 (CSS 로드를 기다리지 않고) 즉시 렌더링할 컬러 스키마
  ```html
  <meta name="color-scheme" content="dark light" />
  ```
  - 추가설명
    - [What Does Dark Mode’s “color-scheme” Actually Do?](https://medium.com/dev-channel/what-does-dark-modes-supported-color-schemes-actually-do-69c2eacdfa1d)
    - [웹에서 다크모드 구현하기](https://marshall-ku.com/web/tips/%EC%9B%B9%EC%97%90%EC%84%9C-%EB%8B%A4%ED%81%AC-%EB%AA%A8%EB%93%9C-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

## OG(Open Graph)

> 페이스북이 만든 메타 데이터 정의 프로토콜으로, 웹 페이지를 소셜 그래프에서 표현하기 최적화된 형태의 오브젝트로 설정한다.

- 추가설명
  - [The Open Graph protocol](https://ogp.me/)
  - [트위터 카드(Twitter Cards)](https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/abouts-cards)
  - [Meta Tags (generator)](https://metatags.io/)

### Basic Metadata

- `og:title`: 그래프 상에 보여줄 오브젝트의 제목
  ```html
  <meta property="og:title" content="인테리어 집꾸미기는 오늘의집" />
  ```
- `og:type`: 오브젝트의 타입
  ```html
  <meta property="og:type" content="website" />
  ```
- `og:url`: 그래프에서 영구 ID(permanent ID)로 사용될 오브젝트의 [canonical URL](https://support.google.com/webmasters/answer/10347851?hl=en)
  ```html
  <meta property="og:url" content="https://ohou.se/" />
  ```
- `og:image`: 그래프 상에 보여줄 오브젝트를 표현하는 이미지 URL
  ```html
  <meta
    property="og:image"
    content="https://s3-ap-northeast-1.amazonaws.com/bucketplace-v2-development/uploads/default_images/open_graph_icon_2.png"
  />
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### Optional Metadata

- `og:audio`: 오브젝트와 함께 제공되는 오디오 파일 URL

  ```html
  <meta property="og:audio" content="https://example.com/bond/theme.mp3" />
  ```

- `og:description`: 오브젝트에 대한 1~2 문장의 설명

  ```html
  <meta
    name="description"
    content="2000만이 선택한 No.1 인테리어 필수앱. 집들이 구경부터 제품 정보 확인, 구매까지 한 번에!"
  />
  ```

- `og:locale`: 태그가 마크업된 지역 정보 (기본값은 `en_US`)

  ```html
  <meta property="og:locale" content="ko_KR" />
  ```

- `og:locale:alternate`: 페이지를 사용할 수 있는 다른 지역들

  ```html
  <meta property="og:locale:alternate" content="fr_FR" />
  <meta property="og:locale:alternate" content="es_ES" />
  ```

- `og:site_name`: 오브젝트가 어떠한 상위 사이트의 일부분인 경우 나타낼 전체 사이트의 이름

  ```html
  <meta property="og:site_name" content="IMDb" />
  ```

- `og:video`: 페이지를 설명하는 비디오 URL
  ```html
  <meta property="og:video" content="https://example.com/bond/trailer.swf" />
  ```

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

> HTML에 특수 문자를 표시하는 방법이다. 
>
> 엔티티 코드를 사용하지 않고 특수문자를 표기한다면 오류가 발생할 수 있으니 엔티티 코드를 사용하는 것이 좋다.

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

## 이미지 & 미디어

### 이미지(`<img>`)

- [이미지](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Image_types)를 문서에 삽입한다.
  - `src`: 이미지 경로 (필수)
  - `alt`: 이미지의 텍스트 설명 (필수 아닌 필수)
  - 추가설명
    - [MDN: `<img>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/img)
  ```html
  <img
    class="fit-picture"
    src="/media/cc0-images/grapefruit-slice-332-332.jpg"
    alt="Grapefruit slice atop a pile of other slices"
  />
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 비디오(`<video>`)

- 비디오 플레이백을 지원하는 미디어 플레이어를 문서에 삽입한다.

  - 추가설명
    - [MDN: `<video>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Video)

  ```html
  <video controls width="250">
    <source src="/media/cc0-videos/flower.webm" type="video/webm" />

    <source src="/media/cc0-videos/flower.mp4" type="video/mp4" />
    쏴리! 니가 사용하고 있는 브라우저가 이 비디오를 지원하지 않네.
  </video>
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 오디오(`<audio>`)

- 소리 콘텐츠를 문서에 삽입한다.
  - 추가설명
    - [MDN: `<audio>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/audio)
  ```html
  <figure>
    <figcaption>Listen to the T-Rex:</figcaption>
    <audio controls src="/media/cc0-audio/t-rex-roar.mp3">
      Your browser does not support the
      <code>audio</code> element.
    </audio>
  </figure>
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>
