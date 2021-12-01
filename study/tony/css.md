## CSS Shorthand


### margin & padding

```
margin: 전체
margin: y축  x축
margin: 위↑  x축  아↓
margin: 위↑  오→  아↓  왼←


padding: 전체
padding: y축  x축
padding: 위↑  x축  아↓
padding: 위↑  오→  아↓  왼←
```


### background

```
background: 색깔  이미지  반복설정  위치
```


### font

```
font: 스타일  굵기  크기  줄높이  글꼴
```


### text-decoration

```
text-decoration: 밑줄설정(여러개도 가능)
text-decoration: 밑줄설정  색깔
text-decoration: 스타일  밑줄설정  색깔
text-decoration: 스타일  밑줄설정  색깔  두께
```


### border

```
border: 굵기  스타일  색깔
```


### transition

```
transition: 속성이름  지속시간
transition: 속성이름  지속시간  시간함수(timing function)
transition: 속성이름  지속시간  지연시간(시간 단위일 경우)
transition: 속성이름  지속시간  시간함수  지연시간
```


### animation

```
animation: 지속시간  애니메이션이름
animation: 지속시간  시간함수  지연시간  애니메이션이름
animation: 지속시간  시간함수  지연시간  반복횟수 방향  실행전후스타일적용  진행상태  애니메이션이름
```


### flex

```
추가 예정
```


### grid

```
추가 예정
```

# selector

> CSS 규칙을 적용할 요소를 정의하는 것


### 구분

| 키워드 | 의미 |
| ------ | ---- |
| `*`    | 전체 |
| `elementname`    | 요소(태그) |
| `.classname`    | 클래스 |
| `#idname`    | 아이디 |
|`selectorA   selectorB`| 자손 결합자 |
|`selectorA > selectorB`| 자식 결합자 |
|`selectorA ~ selectorB`| 일반 형제 결합자 |
|`selectorA + selectorB`| 인접 형제 결합자 |


### 우선 순위

| 순위 | 대상 | 점수 |
| ---- | ---- | ---- |
|  1   | `!important` | 최우선 |
|  2   | `인라인 스타일링` | 1000 |
|  3   | `#아이디 선택자` | 100 |
|  4   |  `.클래스 선택자` | 10 |
|  5   |  `의사 클래스` | 10 |
|  6   |  `요소 선택자` | 1 |

`코드 라인 순서`가 가장 마지막으로 영향이 있음


## 의사 클래스 및 의사 요소

>
> 의사 클래스(`:`)는 특정 상태에 스타일을 적용할 때 사용
>
> 의사 요소(`::`)는 특정 부분에 스타일을 적용할 때 사용
>

### 의사 클래스

[현재 모든 엔진에서 지원하는 의사 클래스 목록](https://html.spec.whatwg.org/multipage/semantics-other.html#pseudo-classes
)

- `:defined`
- `:link`
- `:visited`
- `:active`
- `:hover`
- `:focus`
- `:target`
- `:enabled`
- `:disabled`
- `:checked`
- `:indeterminate`
- `:default`
- `:invalid`
- `:in-range`
- `:out-of-range`
- `:required`
- `:optional`
- `:autofill`
- `:read-only`
- `:read-only`
- `:read-write`

[의사 클래스 더보러가기](https://developer.mozilla.org/ko/docs/Web/CSS/Pseudo-classes#%ED%91%9C%EC%A4%80_%EC%9D%98%EC%82%AC_%ED%81%B4%EB%9E%98%EC%8A%A4_%EC%83%89%EC%9D%B8)

### 의사 요소

- `::after`
- `::before`
- `::first-letter`
- `::first-lin`
- `::placeholder`
- `::selection`

[의사 요소 더보러가기](https://developer.mozilla.org/ko/docs/Web/CSS/Pseudo-elements#%ED%91%9C%EC%A4%80_%EC%9D%98%EC%82%AC_%EC%9A%94%EC%86%8C_%EC%83%89%EC%9D%B8)


