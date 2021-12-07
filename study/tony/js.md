# 실행 컨텍스트 (Execution Context)

## Q. 실행 컨텍스트가 뭔가요?

>
> A. 실행 가능한 자바스크립트 코드가 동작하는 추상화된 환경 혹은 공간을 의미 합니다.
>

추가 설명
- 실행 가능한 자바스크립트의 예시로는 전역(global), 함수(function), ~~이발(eval)~~ 가 있습니다.

예시 설명
1. 처음 자바스크립트 코드가 동작하면서 전역 컨텍스트가 생성됩니다.
2. 동작 과정 중에 함수의 선언및 호출이 발생하면, 전 단계에서 생성된 전역 컨텍스트의 위에 함수 컨텍스트가 생성된다.
3. 이러한 과정을 통해 코드 및 컨텍스트가 종료될 때 까지, 스택의 형태로 구성되어 관리된다.


## Q. 실행 컨텍스트의 구성에 대해 설명해주세요.

>
> A. 변수 객체, 스코프 체인, 디스, 이렇게 3가지 속성으로 구성됩니다.
>


예시 설명

```javascript
var name = 'tony'                 // 01
function greeting(word) {         // 02
  console.log(word + ' ' + name)  // 03
}                                 // 04
function comeAcross() {           // 05
  var name = 'eric'               // 06
  console.log(name)               // 07
  greeting('game')                // 08
}                                 // 09
comeAcross()                      // 10


// 01 ~ 09줄
// JS 코드가 동작하면서 전역 컨텍스트가 생성된다.
// 전역 컨텍스트 객체에 다음과 같이 설정된다.
/* 
  '전역 컨텍스트': {
    변수객체: {
      arguments: null,
      variable: ['name', 'greeting', 'comeAcross'], // 초기화 후 =>  variable: [{ name: 'tony' }, { greeting: Function }, { comeAcross: Function }]  이렇게 바뀜
    },
    스코프체인: ['전역 변수객체'],
    디스: window,
  }
*/

// 10줄
// comeAcross 이 호출되는 순간 함수 컨텍스트가 생성된다.
// 해당 함수 컨텍스트 객체에 다음과 같이 설정된다.
/*
  'comeAcross 컨텍스트': {
    변수객체: {
      arguments: null,
      variable: ['name'], => 초기화 후 => [{ name: 'eric' }]가 됨
    },
    scopeChain: ['comeAcross 변수객체', '전역 변수객체'],
    this: window,
  }
*/

// 05 ~ 07줄
// comeAcross 함수 컨텍스트 내부적으로 참조 값을 찾아가며 실행됨.
// ex) 07줄의 name은 함수 컨텍스트의 variable의 name에서 확인 가능 => console log 동작


// 08줄
// greeting 가 호출되는 순간 함수 컨텍스트가 생성된다.
// 해당 함수 컨텍스트는 다음과 같이 설정된다.
/*
  'greeting 컨텍스트': {
    변수객체: {
      arguments: [{ word: 'game'}],
      variable: null,
    },
    scopeChain: ['greeting 변수객체', '전역 변수객체'],
    this: window,
  }
*/

// 02 ~ 03줄
// greeting 함수 컨텍스트 내부적으로 참조 값을 찾아가며 실행됨.
// ex) 03줄의 word는 함수 컨텍스트의 arguments의 word에서 확인 가능,
// name은 변수 객체에서 찾을 수 없기 때문에, 스코프 체인을 따라서 전역 변수객체를 확인하게 됨.
// 그렇기 때문에 comeAcross 함수와는 무관하게 전역 변수객체의 컨텍스트를 확인하므로 tony라는 글자를 확인.
```

## 참조
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/var
- https://poiemaweb.com/js-execution-context
- https://www.zerocho.com/category/JavaScript/post/5741d96d094da4986bc950a0
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this