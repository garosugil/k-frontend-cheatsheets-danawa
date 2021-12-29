[toc]

### 커링 (Currying)

> [Currying?](https://en.wikipedia.org/wiki/Currying)
>
> 수학 그리고 컴퓨터 과학에서 사용되는 용어로써
> 여러 개의 인자를 받는 함수를 하나의 인자만 받는 함수들로 변환하는 테크닉을 말함
>
> 일반적인 용어인만큼 자바스크립트뿐만 아니라 다른 언어에서도 사용됨

- 커링의 일반적인 형태: `f(a, b, c)` => `f(a)(b)(c)`
- 커링의 핵심은 하나 이상의 매개변수를 고정시켜놓은 부분 함수를 만들어서,
  후 부분 함수를 호출할 때마다 해당 매개변수들을 재활용하여 함수의 재사용성을 높이는 것

- 예시

  ```javascript
  function curry(f) {
    return function (a) {
      return function (b) {
        return f(a, b);
      };
    };
  }

  function sum(a, b) {
    return a + b;
  }

  let curriedSum = curry(sum);

  console.log(curriedSum(1)(2)); // 3
  ```

  ```javascript
  const lowerCaseOf = (input) => input.toLowerCase();
  const includes = (what) => (where) => where.includes(what);

  const isIcedBeverage = (input) => includes('iced')(lowerCaseOf(input));
  const filter = (checker) => (list) => list.filter(checker);

  const beverages = ['Iced Latte', 'Hot Americano', 'Iced Cappuccino'];
  const filterIcedBeverage = filter(isIcedBeverage);

  console.log(filterIcedBeverage(beverages)); // [ 'Iced Latte', 'Iced Cappuccino' ]
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 함수 (Functions)

#### 자바스크립트 함수의 특성

- 자바스크립트 함수는 일급 객체 (first-class citizens)에 해당함
  - 일급 객체?
    - 함수의 매개변수로 전달 가능해야 하며
    - 함수의 반환값으로 사용 가능해야 하며
    - 할당 구문에서 사용 가능해야 함 (즉, 변수에 할당 가능)
  - (참고) Higher-Order Functions
    - 함수형 프로그래밍에서 HOF는 "함수를 인자로 받아서, 함수를 반환하는 함수"를 말함
- 모든 함수는 Function 객체에 해당함
- 기본 반환 값은 `undefined`에 해당함

#### 함수의 속성들 (Properties)

- 함수의 이름(name)은 `.name`으로 사용 가능

```javascript
function sayName() {
  console.log(sayName.name);
}

sayName(); // sayName
```

- 함수의 길이(length)는 매개변수의 개수로써 `.length`로 사용 가능
  - (단, 나머지 매개변수는 포함하지 않음)

```javascript
function f1(a) {}
function f2(a, b) {}
function multi(a, b, ...args) {}

console.log(f1.length); // 1
console.log(f2.length); // 2
console.log(multi.length); // 2
```

- 이외에 커스텀 속성도 필요 시 추가 가능

```javascript
function sayName() {
  sayName.age = 100;
}

sayName();
sayName.age; // 100
```

#### 함수 표현식 (Function Expression)

- 함수를 표현식 안에 작성하는 방식

```javascript
let sum1 = function (a, b) {
  // 익명 함수 (anonymous function)
  return a + b;
};

let sum2 = function mySum(a, b) {
  // 기명 함수 (named function)
  return a + b;
};
```

- 기명 함수 표현식은 재귀 호출 등을 위해 사용
  - (단, 해당 이름은 외부에서 접근 불가능함)

```javascript
let greeting = function namedFunc(name) {
  namedFunc(`반가워요! ${name}`); // 재귀 호출
};

greeting('꿈돌이');

namedFunc('꿈돌이'); // Uncaught ReferenceError: namedFunc is not defined
```

#### 함수 선언식 (Function Declaration)

- 함수를 별도의 선언식으로 작성하는 방식

```javascript
function sum(a, b) {
  return a + b;
}
```

#### 함수 표현식 vs. 함수 선언식

- 코드 상에서 함수 호출이 가능한 시점이 다름

```javascript
// 함수 선언식

sum(1, 2); // 3

function sum(a, b) {
  return a + b;
}
```

```javascript
// 함수 표현식

sum(1, 2); // Uncaught ReferenceError: sum is not defined

const sum = function (a, b) {
  return a + b;
};
```

#### 인자와 매개변수 (arguments and parameters)

- 기본 인자 사용 가능

```javascript
function sum1(a, b = 3) {
  return [a, b];
}

function sum2(a = 3, b) {
  return [a, b];
}

sum1(1); // [1, 3]
sum2(1); // [1, undefined]
```

- 정의된 인자의 개수보다 더 많은 값들을 넘겨도 동작함

```javascript
function sum(a, b) {
  return a + b;
}

sum(1, 2, 3, 4, 5); // 1, 2만 계산됨
```

- 나머지 매개변수(rest parameters)는 항상 마지막에 위치해야하며 유일해야함

```javascript
function sum(a, b, ...args) {
  // args는 배열 형태
  // ...
}
```

- arguments vs. 나머지 매개변수

  - arguments 변수는 유사 배열(array-like) 객체로써 배열 관련 메서드 사용이 불가능함

  - 나머지 매개변수는 실제 배열이므로 배열 관련 메서드 사용이 가능함

  - arguments 변수는 모든 매개변수를 담고 있음

```javascript
function sum1(a, b, c) {
  console.log(arguments);
}

function sum2(a, b, ...args) {
  console.log(args);
}

sum1(1, 2, 3); // Arguments(3) [1, 2, 3]
sum2(1, 2, 3); // [3]
```

#### Arrow Functions

> [참고자료](https://hacks.mozilla.org/2015/06/es6-in-depth-arrow-functions/)

- 화살표 함수는 익명 함수로만 작성 가능

- `this`, `arguments`, `super` 등을 가지고 있지 않음

  - **[중요] 화살표 함수 전까지 `this` 는 constructor 안에서는 새롭게 만들어지는 객체를, `strict mode`에서는 `undefined` 값으로, 그리고 어떤 객체의 메서드로써 호출된 함수는 해당 객체를 가리키는 값으로 설정됐었음**

```javascript
// 아래의 this는 일반 모드에서 window 객체에 해당함

function Person() {
  // The Person() constructor defines `this` as itself.
  this.age = 0;

  setInterval(function growUp() {
    console.log(this);
    // In nonstrict mode, the growUp() function defines `this`
    // as the global object, which is different from the `this`
    // defined by the Person() constructor.
    this.age++;
  }, 1000);
}

var p = new Person();
```

```javascript
// 화살표 함수 등장 전에는 아래와 같이 hacky한 방식으로 처리
// 또는 bind 메서드를 사용하여 bound function을 생성하기도 함

function Person() {
  var self = this; // Some choose `that` instead of `self`.
  // Choose one and be consistent.
  self.age = 0;

  setInterval(function growUp() {
    // The callback refers to the `self` variable of which
    // the value is the expected object.
    self.age++;
  }, 1000);
}
```

```javascript
function Person() {
  this.age = 0;

  setInterval(() => {
    this.age++; // |this| properly refers to the person object
  }, 1000);
}

var p = new Person();
```

#### 화살표 함수에 "this"가 없다는 것

- 함수에서 [lexical scope](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures#lexical_scoping)를 따라서 함수 바깥의 변수를 찾듯이 바깥의 `this`를 찾아서 사용함
- 엄밀히 말하면 `bind` 함수를 사용하여 `bound`된 함수를 만드는 것과 다름

#### 즉시 실행 함수 (IIFE)

- [IIFE?](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)

  - Immediately Invoked Function Expression

- 함수 정의와 동시에 실행되는 함수를 일컬음
- 활용 예시
  - 글로벌 네임스페이스 오염 방지에 사용
  - 프라이빗 또는 퍼블릭 변수와 메서드를 만들 때 사용 가능
- 예시

```javascript
(function () {
  // ...
})();
```

```javascript
var factorial = (function hideTheCache() {
  var cache = {};

  function factorial(x) {
    if (x < 2) return 1;
    if (!(x in cache)) {
      cache[x] = x * factorial(x - 1);
    }
    return cache[x];
  }

  return factorial;
})();

factorial(6);
// 720

factorial(7);
// 5040
```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 타입 (Types)

- ECMA-262 ('21.11.20) 기준으로 작성됨

#### 원시 타입 (primitives)

- undefined

- null ([참고자료](https://2ality.com/2013/10/typeof-null.html))

  ```javascript
  typeof null === 'object'; // true
  ```

- boolean

- number

  - `+Infinity`, `-Infinity`, `NaN`

- bigInt

- string

- symbol ([참고자료](https://2ality.com/2014/12/es6-symbols.html))

#### 객체 타입 (object)

- 원시 타입에 속하지 않으면서 "속성들의 집합"으로 구성되는 데이터 타입

  - object

### 이것 (this)

#### 엄격 모드에 따른 `this` 키워드

- `non-strict mode`: 객체에 대한 참조값을 가짐
- `strict mode`: 어떤 값이든 가능

#### 글로벌 위치에서의 this (this in Global Context)

- 전역 객체 (window)와 같음

```javascript
console.log(this === window); // true

word = 'love';
console.log(window.word); // 'love'
console.log(this.word); // 'love'
```

#### 함수 안에서의 this (this in Function Context)

- 비엄격모드에서 기본적으로 window 객체를 가리킴
  - **단, 함수가 어떻게 호출되는지에 따라 달라짐**
- apply, call, bind 등을 이용하여 this를 직접 할당하여 사용 가능

```javascript
// 함수 안에서의 this

function func() {
  return this;
}

func() === window; // true
```

```javascript
// apply, call 메서드를 활용하여 this 직접 할당하기

function whatsThis() {
  return this.word;
}

const obj = { word: 'love' };
const word = 'peace';
this.word = word;

whatsThis(); // peace
whatsThis.apply(obj); // love
whatsThis.call(obj); // love
```

#### 화살표 함수에서의 this

- 화살표 함수는 `this`가 없음
- 자신을 감싸고 있는 바로 상위 렉시컬 스코프의 `this`를 가져와서 사용함
  - [call, apply, bind](#call-apply-bind)를 사용하여 `this`를 강제로 바인딩할 수 없음

```javascript
const globalObj = this;
const arrowFunc = () => this;

console.log(globalObj === arrowFunc()); // true
```

```javascript
const obj = { word: 'love' };
const arrowFunc = () => this.word;

arrowFunc(); // undefiined
arrowFunc.call(obj); // undefined
arrowFunc.apply(obj); // undefined

boundArrow = arrowFunc.bind(obj);
boundArrow(); // undefined
```

#### 메서드에서의 this (1)

- 메서드로 정의된 함수에서의 `this`는 해당 `객체`를 가리킴
- 함수가 정의되는 위치와 시점은 상관없음
- 해당 객체의 메서드로써 호출되기만하면 됨

```javascript
const obj = {
  word: 'love',
  sayWord: function () {
    return this.word;
  },
};

obj.sayWord(); // love
```

```javascript
const obj = { word: 'love' };

function sayWord() {
  return this.word;
}

obj.sayWord = sayWord;
obj.sayWord(); // love
```

#### 메서드에서의 this (2)

- `this`에는 가장 가까운 객체가 바인딩됨
- obz 객체가 obj에 속한다고 할지라도, `obz.sayWord` 함수의 `this`에는 `obz` 객체가 바인딩됨

```javascript
const obj = {
  word: 'love',
};

function sayWord() {
  return this.word;
}

obj.sayWord = sayWord;
obj.obz = { word: 'peace', sayWord: sayWord };

obj.obz.sayWord(); // peace
```

### call, apply, bind

#### call

- 함수 호출 시 `this`와 매개변수를 명시적으로 넘길 수 있는 메서드

```javascript
function foo() {
  console.log(this.a);
}

var obj1 = {
  a: 1,
  foo: foo,
};

var obj2 = {
  a: 100,
  foo: foo,
};

obj1.foo(); // 1
obj2.foo(); // 100

obj1.foo.call(obj2); // 100
obj2.foo.call(obj1); // 1
```

#### apply

- 함수 호출 시 `this`와 매개변수를 명시적으로 넘길 수 있는 메서드 (단, call과는 다르게 apply를 통해 호출할 경우 매개변수들을 배열 형태로 넘김)

```javascript
const array = ['a', 'b'];
const elements = [0, 1, 2];
array.push.apply(array, elements);
console.info(array); // ["a", "b", 0, 1, 2]
```

```javascript
const numbers = [5, 6, 2, 3, 7];
let max = Math.max.apply(null, numbers);
```

#### bind

- 함수 호출 시 `this`와 매개변수를 명시적으로 넘길 수 있는 메서드로써, 호출의 결과로 새로운 함수를 반환함

```javascript
function foo(something) {
  this.a = something;
}

var obj1 = {};

var bar = foo.bind(obj1);
bar(2);
console.log(obj1.a); // 2
```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 프록시

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 심볼

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 프로토타입

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>
