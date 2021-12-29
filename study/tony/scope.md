# 스코프

> 현재 실행되는 컨텍스트를 의미
>
> 계층적인 구조를 가지기 때문에, 하위 스코프는 상위 스코프에 접근할 수 있지만 반대는 불가
>
> 다르게 표현하면, 자바스크립트에서 함수는 클로저로 동작하기 때문에 스코프를 생성하므로 함수 내에 정의된 변수는 외부 함수나 다른 함수 내에서는 접근 할 수 없음

```javascript
function exampleFunction() {
    var x = "declared inside function";
    // x는 오직 exampleFunction 내부에서만 사용 가능.
    console.log("Inside function");
    console.log(x);
}

console.log(x);  // 에러 발생
```
