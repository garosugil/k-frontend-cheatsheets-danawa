# [클로저 - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures)

## 어휘적 범위 지정 (Lexical Scoping)

> 💡 `Lexical`이란, 변수가 소스코드 내 어디에서 사용 가능한지 알기 위해, 그 변수가 소스코드 내 어디에서 선언 되었는지 고려한다는 것을 의미한다.
>
> 이때, 중첩된 함수는 외부 범위(scope)에서 선언한 변수에도 접근할 수 있다.
>

```javascript
function init() {
  var name = "Mozilla"; // name은 init에 의해 생성된 지역 변수이다.
  function displayName() { // displayName() 은 내부 함수이며, 클로저다.
    alert(name); // 부모 함수에서 선언된 변수를 사용한다.
  }
  displayName();
}
init();
```

## 클로저 (Closure)

> 💡 `Closure`란, 함수와 함수가 선언된 어휘적 환경의 조합을 의미한다.

```javascript
function makeFunc() {
  var name = "Mozilla";
  function displayName() {
    alert(name);
  }
  return displayName;
}

var myFunc = makeFunc();
// myFunc변수에 displayName을 리턴함
// 유효범위의 어휘적 환경을 유지
myFunc();
// 여기가 정상적으로 실행되지 않을 것 같지만, 잘 됨
// 리턴된 displayName 함수를 실행(name 변수에 접근)
```

### 함수를 만들어내는 공장

```javascript
function makeAdder(x) {
  var y = 1;
  return function(z) {
    y = 100;
    return x + y + z;
  };
}

// add5 와 add10은 모두 클로저라고 부를 수 있다.
// 결론 : 서로 다른 lexical scoping을 가진 closure
var add5 = makeAdder(5);
var add10 = makeAdder(10);
// 클로저에 x와 y의 환경이 저장됨

console.log(add5(2));  // 107 (x:5 + y:100 + z:2)
console.log(add10(2)); // 112 (x:10 + y:100 + z:2)
// 함수 실행 시 클로저에 저장된 x, y값에 접근하여 값을 계산
```

## 실용적인 클로저

> 💡 결국 클로저는 `특별한 환경` 을 가진 `함수` 를 의미하기 때문에, 다음과 같이 활용 할 수 있다.

```javascript
function makeSizer(size) {
  return function() {
    document.body.style.fontSize = size + 'px';
  };
}

// body 요소의 글자 크기를 바꾸는 함수를 만들고
var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16);

// 특정 요소에 연결할 수 있음
document.getElementById('size-12').onclick = size12;
document.getElementById('size-14').onclick = size14;
document.getElementById('size-16').onclick = size16;
```
