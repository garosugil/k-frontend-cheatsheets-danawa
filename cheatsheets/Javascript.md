# JavaScript 치트시트

- [JavaScript 치트시트](#javascript-치트시트)
  - [기초](#기초)
    - [`let` & `const`](#let--const)
    - [구조 분해 할당(Destructuring Assignment)](#구조-분해-할당destructuring-assignment)
      - [배열 분해](#배열-분해)
      - [객체 분해](#객체-분해)
    - [템플릿 리터럴(Template Literal)](#템플릿-리터럴template-literal)
    - [옵셔널 체이닝(Optional Chaining) 연산자](#옵셔널-체이닝optional-chaining-연산자)
    - [널 병합(Nullish Coalescing) 연산자](#널-병합nullish-coalescing-연산자)
  - [심화](#심화)
    - [클래스(Class)](#클래스class)
    - [모듈(Module)](#모듈module)
    - [Set](#set)
    - [Map](#map)
  - [활용](#활용)
    - [프로미스(Promise)](#프로미스promise)
    - [async & await](#async--await)
    - [Fetch API](#fetch-api)

## 기초

### `let` & `const`

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 구조 분해 할당(Destructuring Assignment)

> 객체나 배열에 저장된 데이터 일부를 "분해"하여 변수에 "할당"한다.

#### 배열 분해

- 이터러블(iterable)에서 필요한 요소만 추출하고 싶을 때 유용하다.

  ```javascript
  let arr = ['Joe', 'Biden'];

  let [firstName, familyName] = arr;
  console.log(firstName); // "Joe"
  console.log(familyName); // "Biden"
  ```

- 쉼표를 사용하여 특정 요소를 무시할 수 있다.

  ```javascript
  let [left, , right] = [1, 2, 3];
  console.log(left); // 1
  console.log(right); // 3
  ```

- 할당 연산자 **우측**에 모든 **이터러블**이 올 수 있다.

  ```javascript
  let [a, b, c] = '바이든';
  console.log(a); // "바"
  console.log(b); // "이"
  console.log(c); // "든"
  ```

- 할당 연산자 **좌측**에 **할당할 수 있는 모든 것(assignables)**이 올 수 있다.

  ```javascript
  let president = {};
  [president.firstName, president.familyName] = '조 바이든'.split(' ');
  console.log(president); // {firstName: '조', familyName: '바이든'}
  ```

- 할당할 값이 없으면 `undefined`로 처리된다.

  ```javascript
  let [firstName, familyName] = [];
  console.log(firstName); // undefined
  console.log(familyName); // undefined
  ```

- 기본값(default value)을 설정할 수 있다.

  ```javascript
  let [firstName = '아무개', familyName = '김'] = ['두한'];
  console.log(firstName); // "두한"
  console.log(familyName); // "김"
  ```

- Rest 프로퍼티를 활용할 수 있다.
  ```javascript
  let numbers = [1, 2, 3, 4, 5];
  let [first, ...restNumbers] = numbers;
  console.log(first); // 1
  console.log(restNumbers); // [2, 3, 4, 5]
  ```

#### 객체 분해

- 객체에서 필요한 프로퍼티 값만 추출하고 싶을 때 유용하다.

  ```javascript
  let president = {
    fullName: '조 바이든',
    age: 79,
  };

  let { age, fullName } = president; // 순서 상관 없음
  console.log(age); // 79
  console.log(fullName); // "조 바이든"
  ```

- 분해한 프로퍼티를 **새로운 변수 이름**으로 할당할 수 있다.

  ```javascript
  let president = {
    full_name: '조 바이든',
    age_count: 79,
  };

  // { 프로퍼티 키: 새로운 변수명 }
  let { full_name: fullName, age_count: age } = president;
  console.log(fullName); // "조 바이든"
  console.log(age); // "79"
  ```

- 할당 연산자(`=`)를 사용해 기본값을 설정할 수 있다.

  ```javascript
  let joeBiden = {
    fullName: '조 바이든',
  };

  let { fullName = '김 아무개', age = 10 } = joeBiden;
  console.log(fullName); // "조 바이든"
  console.log(age); // 10
  ```

- 새로운 변수 이름과 할당 연산자를 동시에 사용할 수 있다.

  ```javascript
  let joeBiden = {
    full_name: '조 바이든',
  };

  let { full_name: fullName = '김 아무개', age_count: age = 10 } = joeBiden;
  console.log(fullName); // "조 바이든"
  console.log(age); // 10
  ```

- Rest 프로퍼티를 활용할 수 있다.

  ```javascript
  const appleDevices = {
    phone: '아이폰',
    laptop: '맥북',
    tablet: '아이패드',
  };
  const { phone, ...restDevices } = appleDevices;
  console.log(phone); // "아이폰"
  console.log(restDevices); // {laptop: '맥북', tablet: '아이패드'}
  ```

- 중첩 객체 구조 분해

  - 객체나 배열이 다른 객체나 배열을 포함하는 경우에도 정보를 추출할 수 있다.

  ```javascript
  let joeBiden = {
    // 중첩 객체
    name: {
      firstName: '조',
      familyName: '바이든',
    },
    // 중첩 객체
    contact: {
      website: 'https://www.whitehouse.gov/contact/',
    },
    // 중첩 배열
    items: ['아이폰', '맥북'],
  };

  const {
    name: { firstName, familyName },
    items: [itemOne, itemTwo],
  } = joeBiden;
  console.log(firstName, familyName); // "조 바이든"
  console.log(itemOne, itemTwo); // "아이폰 맥북"
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 템플릿 리터럴(Template Literal)

- 백틱(``)을 사용하는 문자열 표기법이다.
- 멀티라인 문자열(multi-line strings), 표현식 삽입(expression interpolation) 등 여러 기능을 사용할 수 있다.

  - 멀티라인 문자열

    ```javascript
    // 템플릿 리터럴의 줄바꿈(개행)
    const president = `도널드
    트럼프`;

    // 일반 문자열의 줄바꿈 => 이스케이프 시퀀스 사용
    const newPresident = '조\n바이든';
    ```

  - 표현식 삽입
    ```javascript
    const joeBiden = {
      age: 75,
    };
    const president = `조 바이든의 나이는 ${joeBiden.age + 4}세 입니다.`;
    // "조 바이든의 나이는 79세 입니다."
    ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 옵셔널 체이닝(Optional Chaining) 연산자

- 프로퍼티가 없는 중첩 객체를 "에러 없이" 안전하게 접근할 수 있다.

  - 추가설명
    - [MDN | 옵셔널 체이닝 연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

  ```javascript
  let joeBiden = {
    name: {
      firstName: '조',
      familyName: '바이든',
    },
    pets: {
      dog: {
        name: '백구',
        age: '1',
      },
    },
  };

  // name 프로퍼티가 undefined 또는 null이면 평가를 멈추고 undefined를 반환한다.
  const familyName = joeBiden.name?.familyName;
  console.log(familyName); // "바이든"

  // pets 프로퍼티가 undefined 또는 null이면 평가를 멈추고 undefined를 반환한다. (-> cat도 동일)
  const catName = joeBiden.pets?.cat?.name;
  console.log(catName); // undefined
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 널 병합(Nullish Coalescing) 연산자

- 왼쪽 피연산자가 `undefined` 또는 `null`이면 오른쪽 피연산자를 반환하고, 그렇지 않으면 왼쪽 피연산자를 반환한다.
- 변수에 기본값을 설정할 때 유용하다.

  - 참고자료
    - [MDN | 널 병합 연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)

  ```javascript
  const left = null;
  const right = 'default string';

  // 널 병합 연산자로 구현한 코드
  const result1 = left ?? right;
  console.log(result1); // "default string"

  // 널 병합 연산자 없이 구현한 코드
  const result2 = left !== null && left !== undefined ? left : right;
  console.log(result2); // "default string"
  ```

- `??` vs `||`

  ```javascript
  // ??
  // => 왼쪽 피연산자가 undefined 또는 null이면 오른쪽 피연산자를 반환한다.
  0 ?? 'right'; // 0
  null ?? 'right'; // "right"

  // ||
  // => 왼쪽 피연산자가 Falsy값(false, undefined, null, 0, ...)이면 오른쪽 피연산자를 반환한다.
  0 || 'right'; // "right"
  null || 'right'; // "right"
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

## 심화

### 클래스(Class)

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 모듈(Module)

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### Set

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### Map

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

## 활용

### 프로미스(Promise)

- `Promise` 객체는 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타낸다.
  - `Promise`
    - 비동기 처리를 위한 표준 빌트인 객체 (ES6)
  - `executor(실행 함수)`
    - 비동기 처리를 수행할 콜백 함수.
    - 성공하면 `resolve`, 실패하면 `reject` 함수를 실행한다.
  ```javascript
  new Promise(executor);
  ```
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

<br>

- 프로미스는 비동기 처리 진행 상황을 나타내는 **상태 정보**를 갖는다.
  - `pending`: 비동기 처리가 **실행되지 않은** 상태 (초기 상태)
  - `fulfilled`: 비동기 처리에 **성공**한 상태 (`resolve` 함수 호출)
  - `rejected`: 비동기 처리에 **실패**한 상태 (`reject` 함수 호출)

<br>

- 프로미스의 상태 정보가 바뀌면 후속 처리 메서드(`then`, `catch`, `finally`)를 통해 다음에 수행할 콜백 함수를 호출한다.

  - Promise.prototype`.then`

    - 첫 번째 파라미터: 프로미스가 성공(`resolve`)했을 때 실행되는 콜백 함수
    - 두 번째 파라미터: 프로미스가 실패(`reject`)했을 때 실행되는 콜백 함수

    ```javascript
    const promise = new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve('fulfilled!');
      }, 3000);
    });

    promise.then(
      (result) => console.log(result), // 3초 후 "fulfilled!" 출력
      (error) => console.log(error) // 실행되지 않음
    );
    ```

  - Promise.prototype`.catch`

    - 첫 번째 파라미터: 프로미스가 실패했을 때 실행되는 콜백 함수

    ```javascript
    const promise = new Promise((resolve, reject) => {
      setTimeout(() => {
        reject('rejected!');
      }, 3000);
    });

    promise.catch((error) => console.log(error)); // 3초 후 "rejected!" 출력
    ```

  - Promise.prototype`.finally`
    - 첫 번째 파라미터: 프로미스의 성공 또는 실패와 상관 없이 무조건 한 번 실행되는 콜백 함수
    ```javascript
    new Promise((resolve, reject) => {}).finally(() => console.log('finally!'));
    ```

<br>

- 순차적으로 처리해야 하는 비동기 작업이 여러 개 있는 경우 **프로미스 체이닝(Promise Chaining)**을 통해 해결할 수 있다.

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

<br>

- 프로미스의 5가지 정적 메서드

  - Promise`.all`

    - 여러 개(iterable)의 프로미스를 병렬로 실행시키고, 모든 처리가 성공할 때까지 기다린다.
    - 프로미스들 중 가장 먼저 실패한 프로미스의 에러 내용이 catch로 전달된다.
    - 추가설명
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
      new Promise((resolve, reject) => setTimeout(() => reject('error'), 2000)),
      new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
    ])
      .then(console.log)
      .catch(console.log); // "error"
    ```

  - Promise`.race`

    - 여러 개의 프로미스를 병렬로 실행시키고, 가장 먼저 성공한 프로미스를 기다린다.
    - 프로미스들 중 가장 먼저 실패한 프로미스의 에러 내용이 catch로 전달된다.
    - 추가설명
      - [MDN: Promise.race()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)

    ```javascript
    Promise.race([
      new Promise((resolve, reject) => setTimeout(() => resolve('김씨'), 3000)),
      new Promise((resolve, reject) => setTimeout(() => resolve('이씨'), 2000)),
      new Promise((resolve, reject) => setTimeout(() => resolve('유씨'), 1000)),
    ]).then(console.log); // "유씨"
    ```

  - Promise`.allSettled`

    - 여러 개의 프로미스를 병렬로 실행시키고, 모든 프로미스가 '처리(settled)'될 때까지 기다린다.

    ```javascript
    Promise.allSettled([
      new Promise((resolve, reject) => setTimeout(() => resolve('성공'), 3000)),
      new Promise((resolve, reject) => setTimeout(() => reject('실패'), 2000)),
      new Promise((resolve, reject) => setTimeout(() => resolve('성공'), 1000)),
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
    - 추가설명
      - [MDN: Promise.resolve()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve)
      - [MDN: Promise.reject()]()
    ```javascript
    const resolvedPromise = new Promise((resolve) => resolve([1, 2, 3]));
    resolvedPromise.then(console.log);
    ```

- 프로미스의 에러 핸들링

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### async & await

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### Fetch API

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>
