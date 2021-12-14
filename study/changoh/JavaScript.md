# JavaScript Cheatsheet

## Table of Contents

- [JavaScript Cheatsheet](#javascript-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [ECMAScript 2015(ES6)](#ecmascript-2015es6)
    - [`let` & `const` 변수 선언 키워드](#let--const-변수-선언-키워드)
    - [프로미스(Promise)](#프로미스promise)
      - [프로미스 생성](#프로미스-생성)
      - [프로미스 상태 정보](#프로미스-상태-정보)
      - [후속 처리 메서드(then/catch/finally)](#후속-처리-메서드thencatchfinally)
      - [프로미스 체이닝](#프로미스-체이닝)
      - [프로미스 메서드](#프로미스-메서드)
      - [프로미스의 에러 핸들링](#프로미스의-에러-핸들링)
    - [Fetch API](#fetch-api)
    - [async & await](#async--await)
    - [템플릿 리터럴(Template Literal)](#템플릿-리터럴template-literal)
    - [클래스(Class)](#클래스class)
    - [디스트럭처링(Destructuring)](#디스트럭처링destructuring)
    - [모듈(Module)](#모듈module)
    - [객체 리터럴(Object Literal)](#객체-리터럴object-literal)
    - [배열 고차 함수](#배열-고차-함수)
    - [Set & Map 오브젝트](#set--map-오브젝트)
      - [Set](#set)
      - [Map](#map)
    - [연산자(Operators)](#연산자operators)
      - [옵셔널 체이닝(Optional Chaining) 연산자](#옵셔널-체이닝optional-chaining-연산자)
      - [널 병합(Nullish Coalescing) 연산자](#널-병합nullish-coalescing-연산자)
    - [참고자료](#참고자료)

<br>

---

<br>

## ECMAScript 2015(ES6)

### `let` & `const` 변수 선언 키워드

<br>

---

<br>

### 프로미스(Promise)

#### 프로미스 생성

- 기본 구문
  ```javascript
  new Promise(executor);
  ```
  - `Promise`
    - 비동기 처리를 위한 표준 빌트인 객체 (ES6)
  - `executor(실행 함수)`
    - 비동기 처리를 수행할 콜백 함수.
    - 성공하면 `resolve`, 실패하면 `reject` 함수를 실행한다.
- 예시 코드
  ```javascript
  const promise = new Promise((resolve, reject) => {
    // 비동기 처리 "성공"한 경우
    if ( /* 성공 조건 */ ) {
      resolve(/* 실행 결과 */)
    }
    // 비동기 처리 "실패"한 경우
    reject(/* 에러 내용 */)
  })
  ```

#### 프로미스 상태 정보

> 프로미스는 비동기 처리 진행 상황을 나타내는 상태 정보를 갖는다.

- `pending`
  - 비동기 처리가 **실행되지 않은** 상태 (초기 상태)
- `fulfilled`
  - 비동기 처리에 **성공**한 상태 (`resolve` 함수 호출)
- `rejected`
  - 비동기 처리에 **실패**한 상태 (`reject` 함수 호출)

#### 후속 처리 메서드(then/catch/finally)

> 프로미스의 상태가 변화하면 `then`, `catch`, `finally` 메서드를 통해 다음에 수행할 콜백 함수를 호출한다.

- Promise.prototype`.then`

  - 첫 번째 파라미터: 프로미스가 성공(`resolve`)했을 때 실행되는 콜백 함수
  - 두 번째 파라미터: 프로미스가 실패(`reject`)했을 때 실행되는 콜백 함수

    ```javascript
    const promise = new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve("fulfilled!");
      }, 3000);
    });

    promise.then(
      (result) => console.log(result), // 3초 후 "fulfilled!" 출력
      (error) => console.log(error) // 실행되지 않음
    );
    ```

- Promise.prototype`.catch`

  - 첫 번째 파라미터:

    ```javascript
    const promise = new Promise((resolve, reject) => {
      setTimeout(() => {
        reject("rejected!");
      }, 3000);
    });

    promise.catch((error) => console.log(error)); // 3초 후 "rejected!" 출력
    ```

- Promise.prototype`.finally`
  - 첫 번째 파라미터: 성공 또는 실패와 상관 없이 무조건 한 번 실행되는 콜백 함수
    ```javascript
    new Promise((resolve, reject) => {}).finally(() => console.log("finally!"));
    ```

#### 프로미스 체이닝

> 순차적으로 처리해야 하는 비동기 작업이 여러 개 있는 경우 프로미스 체이닝(Promise Chaining)을 통해 해결할 수 있다.

```javascript
new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(1);
  }, 1000);
})
  .then((result) => {
    console.log(result); // 1
    return result * 2;
  })
  .then((result) => {
    console.log(result); // 2
    return result * 2;
  })
  .then((result) => {
    console.log(result); // 4
    return result * 2;
  });
```

#### 프로미스 메서드

> Promise는 5가지 정적 메서드를 제공한다.

- Promise`.all`

  - 여러 개(iterable)의 프로미스를 병렬로 실행시키고, 모든 처리가 성공할 때까지 기다린다.
  - 프로미스들 중 가장 먼저 실패한 프로미스의 에러 내용이 catch로 전달된다.
  - [MDN: Promise.all()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

    ```javascript
    Promise.all([
      new Promise((resolve, reject) => setTimeout(() => resolve(1), 3000)),
      new Promise((resolve, reject) => setTimeout(() => resolve(1), 2000)),
      new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
    ]).then(console.log); // [1, 1, 1]
    ```

    ```javascript
    Promise.all([
      new Promise((resolve, reject) => setTimeout(() => resolve(1), 3000)),
      new Promise((resolve, reject) => setTimeout(() => reject("error"), 2000)),
      new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
    ])
      .then(console.log)
      .catch(console.log); // "error"
    ```

- Promise`.race`

  - 여러 개의 프로미스를 병렬로 실행시키고, 가장 먼저 성공한 프로미스를 기다린다.
  - 프로미스들 중 가장 먼저 실패한 프로미스의 에러 내용이 catch로 전달된다.
  - [MDN: Promise.race()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)

    ```javascript
    Promise.race([
      new Promise((resolve, reject) => setTimeout(() => resolve("김씨"), 3000)),
      new Promise((resolve, reject) => setTimeout(() => resolve("이씨"), 2000)),
      new Promise((resolve, reject) => setTimeout(() => resolve("유씨"), 1000)),
    ]).then(console.log); // "유씨"
    ```

- Promise`.allSettled`

  - 여러 개의 프로미스를 병렬로 실행시키고, 모든 프로미스가 '처리(settled)'될 때까지 기다린다.

    ```javascript
    Promise.allSettled([
      new Promise((resolve, reject) => setTimeout(() => resolve("성공"), 3000)),
      new Promise((resolve, reject) => setTimeout(() => reject("실패"), 2000)),
      new Promise((resolve, reject) => setTimeout(() => resolve("성공"), 1000)),
    ]).then(console.log);

    // ✅ 결과
    // [
    //   {status: 'fulfilled', value: '성공'},
    //   {status: 'rejected', reason: '실패'},
    //   {status: 'fulfilled', value: '성공'},
    // ]
    ```

- Promise`.resolve` / Promise`.reject`
  - 이미 존재하는 값을 wrapping하여 성공/실패 상태의 프로미스를 생성한다.
  - async/await 문법이 생긴 뒤로 사용도가 떨어졌다.
  - [MDN: Promise.resolve()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve) / [reject()]()
    ```javascript
    const resolvedPromise = new Promise((resolve) => resolve([1, 2, 3]));
    resolvedPromise.then(console.log);
    ```

#### 프로미스의 에러 핸들링

<br>

---

<br>

### Fetch API

> 네트워크 통신을 포함한 리소스 획득을 위한 인터페이스

<br>

---

<br>

### async & await

- 참고자료
  - [Medium | A Common Misconception About Async/Await in JavaScript](https://betterprogramming.pub/a-common-misconception-about-async-await-in-javascript-33de224bd5f)

<br>

---

<br>

### 템플릿 리터럴(Template Literal)

<br>

---

<br>

### 클래스(Class)

<br>

---

<br>

### 디스트럭처링(Destructuring)

- 참고자료
  - [Medium | Why I Find JavaScript’s Destructuring So Useful](https://betterprogramming.pub/why-i-find-javascripts-destructuring-so-useful-7be41d9ba609)

<br>

---

<br>

### 모듈(Module)

<br>

---

<br>

### 객체 리터럴(Object Literal)

<br>

---

<br>

### 배열 고차 함수

- 참고자료

<br>

---

<br>

### Set & Map 오브젝트

#### Set

#### Map

- 참고자료
  - [Medium | Map, WeakMap, Set, and WeakSet in JavaScript](https://betterprogramming.pub/map-weakmap-set-weakset-in-javascript-77ecb5161e3)

<br>

---

<br>

### 연산자(Operators)

#### 옵셔널 체이닝(Optional Chaining) 연산자

- 참고자료
  - [MDN | 옵셔널 체이닝 연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

#### 널 병합(Nullish Coalescing) 연산자

- 참고자료
  - [MDN | 널 병합 연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)

<br>

---

<br>
### 참고자료

- [Github | es6features](https://github.com/lukehoban/es6features)
- [W3Schools | JavaScript ES6](https://www.w3schools.com/js/js_es6.asp)

<br>

---

<br>