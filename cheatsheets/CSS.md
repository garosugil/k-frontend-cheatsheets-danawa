# CSS Cheatsheet

> CSS 치트시트입니다.

## Table of Contents

---

- [HTML Cheatsheet](#html-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [미디어 쿼리](#미디어 쿼리)

<br>

---

<br>

## 미디어 쿼리

> 미디어 쿼리는 지정한 규칙에 일치하는 경우에만 브라우저 및 장치 환경에 CSS를 적용할 수 있는 방법을 제공한다.

<br>

### `@media media-type and (media-feature-rule){ /* CSS rules */ }`

- 미디어 쿼리 기본 사용 방법이다.

<br>

### 미디어 유형

#### `@media all { /* CSS rules */ } `

- 모든 장치를 대상으로 한다.

<br>

#### `@media screen { /* CSS rules */ }`

- 화면을 대상으로 한다.

<br>

#### `@media print { /* CSS rules */ }`

- 인쇄 결과물 및 출력 미리보기 화면에 표시 중인 문서를 대상으로 한다.

<br>

### 미디어 기능 규칙

#### `@media (width: 600px) { /* CSS rules */ }`

- 해당 width에 CSS 규칙이 적용된다.
- `min-width` 또는 `max-width` 를 사용하여 최소, 최대 너비를 지정할 수 있다.

<br>

#### `@media (height: 400px) { /* CSS rules */ }`

- 해당 높이에 CSS 규칙이 적용된다.
- `min-height` 또는 `max-height` 를 사용하여 최소, 최대 높이를 지정할 수 있다.

<br>

#### `@media (orientation: landscape) { /* CSS rules */ }`

- `orientation` 을 사용하여 세로 모드 또는 가로 모드를 검사할 수 있다.
- `landscape` 는 가로 모드, `portrait` 는 세로 모드

<br>

### 디바이스별 해상도

####`@media all and (min-width: 1024px) { /* CSS rules */ } `

- 미디어 쿼리 PC 해상도

<br>

####`@media all and (min-width: ) and (max-width: ) { /* CSS rules */ }`

- 미디어 쿼리 Tablet 해상도

<br>

####`@media all and (min-width: ) and (max-width: ) { /* CSS rules */ }`

- 미디어 쿼리 Mobile 해상도

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>
