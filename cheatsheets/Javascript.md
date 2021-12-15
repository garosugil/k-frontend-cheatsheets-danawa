# Javascript Cheatsheet

> Javascript 치트시트입니다.

## Table of Contents

---

- [Javascript Cheatsheet](#Javascript-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [조건문](#조건문)
  - [반복문](#반복문)
  - [이벤트](#이벤트)

<br>

---

<br>

## 조건문

> 자바스크립트 조건문

<br>

#### `if`

- `if` 문은 지정한 조건이 참인 경우만 명령문을 실행한다.
- `else if` 를 사용하여 또 다른 조건을 지정할 수 있으며 `else if` 의 갯수 제한은 없다.
- `else` 를 사용하여 위 조건이 거짓일 경우에 명령문을 실행할 수 있다.

```javascript
/* 
	구문
	조건: 참 또는 거짓으로 나타낼 수 있는 표현식이다.
	명령문: 해당 조건이 참일 때 실행되는 문이다.
*/
if (조건1) {
  명령문;
} else if (조건2) {
  명령문;
} else {
  명령문;
}
```

- 예시

```javascript
var num = 10;
if (num >= 10) {
  console.log("숫자는 10 이상이다.");
} else if (0 <= num && num < 10) {
  console.log("숫자는 0 이상 10 미만이다");
} else {
  console.log("숫자는 0 미만이다.");
}
// 숫자는 10 이상이다.
```

<br>

#### `switch`

- `switch` 문은 표현식 지정하여 표현식의 값을 `case` 절과 일치시키고 해당 케이스와 관련된 명령문을 실행시킨다.
- `default` 표현식과 일치하는 `case`가 없을 때 `default` 절의 명령문이 실행된다.
- `break`를 사용하지 않으면 표현식과 일치한 `case` 절의 명령문을 실행한 후 아래의 `case` 절의 명령문을 모두 실행시키기 때문에 `break` 를 사용해야 한다.

```javascript
/*
	구문
	표현식: case 절과 일치시킬 표현식이다.
	값: 해당 case의 값이다.
	명령문: case 절의 값이 표현식과 일치했을 경우 실행되는 구문이다.
*/
switch (표현식) {
  case 값1:
    명령문;
    break;
  case 값2:
    명령문;
    break;
  default:
    명령문;
}
```

- 예시

```javascript
var fruit = "banana";
switch (fruit) {
  case "apple":
    console.log("사과는 빨간색");
    break;
  case "banana":
    console.log("바나나는 노란색");
    break;
  default:
    console.log("사과 또는 바나나를 입력하세요.");
}
// 바나나는 노란색
```

<br>

## 반복문

> 자바스크립트 반복문

#### `for`

- `for` 문은 조건을 지정하여 해당 조건이 참일 경우 반복하여 명령문을 실행하는 문이다.

```javascript
/*
	구문
	초기화: 식 또는 변수 선언.
	조건: 매 반복마다 평가할 식이다. 해당 조건에 부합할 경우에만 명령문이 실행된다.
	평가할 식: 조건 평가 이전에 발생하며 매 반복 후 실행된다.
	명령문: 반복을 수행하는 문으로 조건의 결과가 참일 때 실행된다.
*/
for (초기화; 조건; 평가할 식;) {
    명령문
}
```

- 예시

```javascript
for (var i = 0; i <= 5; i++) {
  console.log(i);
}
/*
0
1
2
3
4
5
*/
```

<br>

#### `while`

- `while` 문은 조건문이 참일 때 실행되는 반복문이다.

```javascript
/*
	구문
	조건: 매 반복마다 평가할 식이다. 반복이 시작되기 전에 조건을 평가한다.
	명령문: 해당 조건이 참일 때만 실행되는 문이다.
*/
while (조건) {
  명령문;
}
```

- 예시

```javascript
var n = 0;
while (n < 3) {
  n += 1;
  console.log(n);
}
/*
1
2
3
*/
```

<br>

#### `do... while`

- `do...while` 문은 조건이 거짓으로 평가될 때까지 지정된 구문을 실행하는 반복문이다.
- 단, `do` 구문이 실행된 후 조건이 평가되기 때문에 구문은 무조건 한 번은 실행된다.

```javascript
/*
	구문
	do 구문: 조건이 참일 때마다 한 번이상 실행되는 구문이다.
	while 조건식: 매 반복마다 평가되는 조건식이다. 조건이 거짓이면 do...while문은 종료된다.
*/
do {
  구문;
} while (조건식);
```

- 예시

```javascript
var result = "";
var i = 0;
do {
  i += 1;
  result += i + " ";
} while (i > 0 && i < 5);

console.log(result);
// 1 2 3 4 5
```

<br>

## 이벤트

<br>

### 이벤트 핸들러

- 이벤트가 발생되면 실행되는 함수
- `addEventListener()` 메서드를 사용하여 이벤트 등록하고 이벤트 핸들러를 생성할 수 있다.
- 예시
  - 버튼 클릭 이벤트 발생시 alert 노출하는 이벤트 핸들러 함수 생성

```html
<body>
  <button>클릭<button>
  <script>
    var btn = document.querySelector("button");

    btn.addEventListener('click', function() {
      alert("버튼을 클릭했습니다!");
    });
  </script>
</body>
```

<br>

### 이벤트 흐름

```
DOM 이벤트에서 정의한 이벤트 흐름 3단계
1. 캡처링 단계
2. 타깃 단계
3. 버블링 단계
```

<br>

#### 이벤트 캡처링

- 이벤트가 `<html>` 요소에서 시작해 자식 요소들로 전파되고 실제 이벤트가 발생한 타깃 요소에 닿을때까지 해당 이벤트가 등록되었는지 자식 요소들을 확인하는 단계를 반복하는 것을 **이벤트 캡처링**이라 한다.
- 캡처링 단계에서 이벤트를 확인하고자 한다면 `addEventListener`의 `capture` 옵션을 `true`로 설정한다.
  - `default` 값은 `false` 이다.

<br>

#### 이벤트 타깃

- 실제 이벤트가 발생한 요소를 **타깃 요소**라고 한다.
- `event.target`을 사용하여 해당 요소에 접근할 수 있다.

<br>

#### 이벤트 버블링

- 어떠한 요소에 이벤트가 발생하면 할당된 핸들러가 동작하고, `<html>` 요소를 거쳐 `document` 객체를 만날 때까지 부모 요소들을 거치며 이벤트가 존재하는지 확인하고 만약 존재한다면 해당 요소에 할당된 핸들러가 동작하는 단계를 반복하는 것을 **이벤트 버블링**이라 한다.

* 예시

```html
<form onclick="alert('form')">
  FORM
  <div onclick="alert('div')">
    DIV
    <p onclick="alert('p')">
      P
    </p>
  <div>
</form>
```

- 동작 순서

```text
1. P를 클릭하면 <p>에 할당된 핸들러가 동작한다.
2. 부모요소인 <div>에 onclick 이벤트가 존재하는지 확인한다.
   onclick 이벤트 핸들러가 존재하므로 할당된 핸들러가 동작한다.
3. <form> 요소에 onclick 이벤트 핸들러가 존재하므로 할당된 핸들러가 동작한다.
4. <html> 요소를 거쳐 document 객체에 닿을 때까지 위 과정을 반복하며 각 요소에 할당된 onclick 핸들러가 동작한다.
```

<br>

#### 이벤트 버블링 중단하기

- `event.stopPropagation()` 이벤트 객체 메서드를 사용하면 이벤트가 발생한 타깃에서 할당된 핸들러가 실행된 후, 부모요소로 거슬러 올라가지 않고 버블링을 중단시킨다.

* 예시

```html
<div onClick="alert('이벤트 버블링 중단')">
  <button onclick="event.stopPropagation()">Click</button>
</div>
```

- 동작

```
'이벤트 버블링 중단' alert은 동작하지 않는다.
```

<br>

#### 이벤트 위임

- 다수의 자식 요소 중 하나를 선택했을 때 이벤트가 실행되기를 원할 때, 모든 자식 요소에게 이벤트를 설정하는 것이 아닌 부모 요소에 이벤트를 등록해 자식 요소의 이벤트까지 관리하는 것을 **이벤트 위임** 이라 한다.

* 예시

```html
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
</ul>
```

<br>
