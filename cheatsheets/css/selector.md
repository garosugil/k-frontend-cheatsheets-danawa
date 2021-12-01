# selector

> CSS 규칙을 적용할 요소를 정의하는 것


## 구분

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


## 우선 순위

1. `!important`
2. `인라인 스타일링`
3. `#아이디 선택자`
4. `.클래스 선택자`
5. `의사 클래스`
6. `요소 선택자`
7. `의사 요소`
8. `코드 라인 순서`

---


# 의사 클래스 및 의사 요소

>
> 의사 클래스(`:`)는 특정 상태에 스타일을 적용할 때 사용
>
> 의사 요소(`::`)는 특정 부분에 스타일을 적용할 때 사용
>

## 의사 클래스

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

## 의사 요소

- `::after`
- `::before`
- `::first-letter`
- `::first-lin`
- `::placeholder`
- `::selection`

[의사 요소 더보러가기](https://developer.mozilla.org/ko/docs/Web/CSS/Pseudo-elements#%ED%91%9C%EC%A4%80_%EC%9D%98%EC%82%AC_%EC%9A%94%EC%86%8C_%EC%83%89%EC%9D%B8)
