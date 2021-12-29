# JavaScript 치트시트

- [JavaScript 치트시트](#javascript-치트시트)
  - [기초](#기초)
    - [`let` & `const`](#let--const)
      - [`let` 키워드](#let-키워드)
      - [`const` 키워드](#const-키워드)
    - [구조 분해 할당(Destructuring Assignment)](#구조-분해-할당destructuring-assignment)
      - [배열 분해](#배열-분해)
      - [객체 분해](#객체-분해)
    - [템플릿 리터럴(Template Literal)](#템플릿-리터럴template-literal)
    - [옵셔널 체이닝(Optional Chaining) 연산자](#옵셔널-체이닝optional-chaining-연산자)
    - [널 병합(Nullish Coalescing) 연산자](#널-병합nullish-coalescing-연산자)
  - [심화](#심화)
    - [클래스(Class)](#클래스class)
    - [모듈(Module)](#모듈module)
      - [Module Scope](#module-scope)
      - [Exports](#exports)
      - [Imports](#imports)
    - [Set](#set)
    - [Map](#map)
  - [활용](#활용)
    - [프로미스(Promise)](#프로미스promise)
    - [async & await](#async--await)
    - [Fetch API](#fetch-api)

## 기초

### `let` & `const`

#### `let` 키워드

- 이름이 동일한 변수를 선언할 수 없다.

  ```javascript
  // let 키워드 : 이름 중복 X

  let president = "조 바이든";
  let president = "도널드 트럼프"; // SyntaxError: Identifier 'president' has already been declared
  console.log(president); // "조 바이든"
  ```

  ```javascript
  // var 키워드 : 이름 중복 O

  var president = "조 바이든";
  var president = "도널드 트럼프";
  console.log(president); // "도널드 트럼프"
  ```

- **블록 레벨 스코프**를 따른다.

  - `let` 키워드
    - **모든 코드 블록(`함수`, `if`문, `for`문 등)**을 **지역 스코프**로 인정한다. (=> 블록 레벨 스코프)

  ```javascript
  let president = "조 바이든"; // 전역 변수

  if (true) {
    let president = "도널드 트럼프"; // 지역 변수
    let actor = "최민식"; // 지역 변수
  }

  console.log(president); // "조 바이든"
  console.log(actor); // ReferenceError: actor is not defined
  ```

  - `var` 키워드
    - **함수 코드 블록**만 **지역 스코프**로 인정한다. (=> 함수 레벨 스코프)
    - 함수 외부에서 var 키워드로 선언하면 모두 전역 변수가 된다.
    - 전역 변수 남발 시 애플리케이션의 복잡도가 증가한다.

  ```javascript
  var president = "조 바이든"; // 전역 변수

  if (true) {
    var president = "도널드 트럼프"; // 전역 변수
    var actor = "최민식"; // 전역 변수
  }

  console.log(president); // "도널드 트럼프"
  console.log(actor); // "최민식"
  ```

- 변수 호이스팅이 발생하지 않는다.

  ```javascript
  // let 키워드 : 호이스팅 X

  console.log(president); // ReferenceError: president is not defined
  let president;
  ```

  ```javascript
  // var 키워드 : 호이스팅 O

  console.log(president); // undefined
  var president;
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

#### `const` 키워드

- `const` 키워드를 사용해 변화하지 않는 변수인 **상수(constant)**를 선언한다.

  ```javascript
  const bestLanguage = "javascript";
  ```

- (let과 동일) 블록 레벨 스코프를 따른다.

- (let과 동일) 호이스팅 되지 않는다.

- 일반적으로 상수의 식별자는 대문자와 언더스코어(`_`)로 선언해 명확히 나타낸다.

  ```javascript
  const BEST_LANGUAGE = "javascript";
  ```

- 선언과 동시에 초기화해야한다.

  ```javascript
  const BEST_LANGUAGE; // SyntaxError: Missing initializer in const declaration
  ```

- 재할당 할 수 없다.

  ```javascript
  const BEST_LANGUAGE = "javascript";
  BEST_LANGUAGE = "javasc"; // TypeError: Assignment to constant variable.
  ```

- 재할당은 안되지만 객체의 값은 변경할 수 있다.

  ```javascript
  // 1
  const PRESIDENT = {
    name: "도널드 트럼프",
  };
  PRESIDENT.name = "조 바이든";
  console.log(PRESIDENT); // {name: '조 바이든'}

  // 2
  const LANGUAGE_LIST = ["javascript"];
  LANGUAGE_LIST.push("python");
  console.log(LANGUAGE_LIST); // ['javascript', 'python']
  ```

-

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

### 구조 분해 할당(Destructuring Assignment)

> 객체나 배열에 저장된 데이터 일부를 "분해"하여 변수에 "할당"한다.

#### 배열 분해

- 이터러블(iterable)에서 필요한 요소만 추출하고 싶을 때 유용하다.

  ```javascript
  let arr = ["Joe", "Biden"];

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
  let [a, b, c] = "바이든";
  console.log(a); // "바"
  console.log(b); // "이"
  console.log(c); // "든"
  ```

- 할당 연산자 **좌측**에 **할당할 수 있는 모든 것(assignables)**이 올 수 있다.

  ```javascript
  let president = {};
  [president.firstName, president.familyName] = "조 바이든".split(" ");
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
  let [firstName = "아무개", familyName = "김"] = ["두한"];
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
    fullName: "조 바이든",
    age: 79,
  };

  let { age, fullName } = president; // 순서 상관 없음
  console.log(age); // 79
  console.log(fullName); // "조 바이든"
  ```

- 분해한 프로퍼티를 **새로운 변수 이름**으로 할당할 수 있다.

  ```javascript
  let president = {
    full_name: "조 바이든",
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
    fullName: "조 바이든",
  };

  let { fullName = "김 아무개", age = 10 } = joeBiden;
  console.log(fullName); // "조 바이든"
  console.log(age); // 10
  ```

- 새로운 변수 이름과 할당 연산자를 동시에 사용할 수 있다.

  ```javascript
  let joeBiden = {
    full_name: "조 바이든",
  };

  let { full_name: fullName = "김 아무개", age_count: age = 10 } = joeBiden;
  console.log(fullName); // "조 바이든"
  console.log(age); // 10
  ```

- Rest 프로퍼티를 활용할 수 있다.

  ```javascript
  const appleDevices = {
    phone: "아이폰",
    laptop: "맥북",
    tablet: "아이패드",
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
      firstName: "조",
      familyName: "바이든",
    },
    // 중첩 객체
    contact: {
      website: "https://www.whitehouse.gov/contact/",
    },
    // 중첩 배열
    items: ["아이폰", "맥북"],
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
    const newPresident = "조\n바이든";
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
      firstName: "조",
      familyName: "바이든",
    },
    pets: {
      dog: {
        name: "백구",
        age: "1",
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
  const right = "default string";

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
  0 ?? "right"; // 0
  null ?? "right"; // "right"

  // ||
  // => 왼쪽 피연산자가 Falsy값(false, undefined, null, 0, ...)이면 오른쪽 피연산자를 반환한다.
  0 || "right"; // "right"
  null || "right"; // "right"
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

- **모듈**은 자바스크립트 애플리케이션을 구성하는 **분리된 코드 조각(개별 파일)**을 의미한다.
  - 자바스크립트는 태생적 한계로 인해 모듈 시스템이 없었기 때문에 파일 스코프, import/export를 지원하지 않았다.
  - 자바스크립트 앱의 발전에 따라 여러 모듈 시스템(`AMD`, `CommonJS`, `UMD`)들이 만들어졌고, Node.js는 `CommonJS`를 사실상 표준으로 채택했다.
  - ES6에서 클라이언트 사이드 자바스크립트에서 동작하는 `ESM(ES6 Module)`이라 불리는 표준 모듈 기능이 추가됐다.

#### Module Scope

- ESM을 활용하여 자바스크립트 모듈을 생성하고 모듈 별로 **독립적인 스코프**를 가질 수 있다.

  - script 태그에 `type="module"` 어트리뷰트를 추가한다.
  - 모듈임을 명확히 하기 위해 파일 확장자는 `.mjs`로 설정한다.

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head> </head>
    <body>
      <script src="script1.mjs" type="module"></script>
      <script src="script2.mjs" type="module"></script>
    </body>
  </html>
  ```

  ```javascript
  // script1.mjs

  const a = "1번 파일의 변수";
  console.log(a); // "1번 파일의 변수"

  const joeBiden = "조 바이든";
  ```

  ```javascript
  // script2.mjs

  // ✅ script1과 변수가 중복돼도 문제가 발생하지 않는다.
  const a = "2번 파일의 변수";
  console.log(a); // "2번 파일의 변수"

  // ✅ 다른 모듈 스코프에 있는 식별자를 참조할 수 없다.
  console.log(joeBiden); // Uncaught ReferenceError: joeBiden is not defined
  ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

#### Exports

- `Named exports`

  - 각 선언부 앞에 `export` 키워드를 작성해 **원하는 식별자**를 모듈 외부에 내보낼 수 있다.
    ```javascript
    export const joeBiden = "조 바이든";
    ```
  - 파일 끝에 한 번만 작성하여 원하는 식별자들을 한 번에 내보낼 수 있다.

    ```javascript
    const joeBiden = "조 바이든";

    export { joeBiden };
    ```

- `Default exports`

  - 선언부 앞에 `export default` 키워드를 작성해 **하나의 값**을 모듈 외부에 내보낼 수 있다.

    - 모듈당 하나만 있을 수 있으므로 이름 없이 내보낼 수 있다.

    ```javascript
    // hello-world.mjs

    export default function () {
      alert("HELLO WORLD");
    }
    ```

    ```javascript
    // presidents.mjs

    export default [
      "노태우",
      "김영삼",
      "김대중",
      "노무현",
      "이명박",
      "박근혜",
      "문재인",
    ];
    ```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

---

<br>

#### Imports

> `import` 키워드를 사용해 다른 모듈에서 내보낸 식별자를 내 스코프로 가져올 수 있다.

- **Named exports 가져오기**

  - **중괄호 안**에 가져올 식별자를 작성한다.

    ```javascript
    import { joeBiden } from "./script1.mjs";
    console.log(joeBiden); // "조 바이든"
    ```

  - `as`를 사용해 원하는 이름으로 바꿀 수 있다.

    ```javascript
    import { joeBiden as doohanKim } from "./script1.mjs";
    console.log(doohanKim); // "조 바이든"
    ```

  - `*` 를 사용해 내보낸 식별자를 한 번에 가져올 수 있다. 하지만 대부분의 경우 구체적으로 명시하는 것이 좋다.

    - 웹팩(webpack)과 같은 모던 빌드 툴의 tree-shaking을 돕는다.
    - `module.function()` 보다 `function()`이 더 간결하다.
    - 어떤 것이 쓰이고 있는지 명확하기 때문에 코드 구조 파악과 리팩터링이 쉽다.

    ```javascript
    import * as scriptOne from "./script1.mjs";
    console.log(scriptOne.joeBiden); // "조 바이든"
    ```

- **Default exports 가져오기**

  - **중괄호(`{}`) 없이 원하는 이름으로** 가져온다.

    ```javascript
    import PRESIDENTS from "./presidents.mjs";
    console.log(PRESIDENTS); // ["노태우", "김영삼", "김대중", "노무현", "이명박", "박근혜", "문재인"]
    ```

- 추가설명
  - [ES6 In Depth: Modules](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/)
  - [ES modules: A cartoon deep-dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)

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
        resolve("fulfilled!");
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
        reject("rejected!");
      }, 3000);
    });

    promise.catch((error) => console.log(error)); // 3초 후 "rejected!" 출력
    ```

  - Promise.prototype`.finally`

    - 첫 번째 파라미터: 프로미스의 성공 또는 실패와 상관 없이 무조건 한 번 실행되는 콜백 함수

    ```javascript
    new Promise((resolve, reject) => {}).finally(() => console.log("finally!"));
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
      new Promise((resolve, reject) => setTimeout(() => reject("error"), 2000)),
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
