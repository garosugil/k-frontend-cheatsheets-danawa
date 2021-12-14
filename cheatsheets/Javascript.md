# Javascript Cheatsheet

> Javascript 치트시트입니다.



## Table of Contents

****

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

* `if` 문은 지정한 조건이 참인 경우만 명령문을 실행한다. 
* `else if` 를 사용하여 또 다른 조건을 지정할 수 있으며 `else if` 의 갯수 제한은 없다.
* `else` 를 사용하여 위 조건이 거짓일 경우에 명령문을 실행할 수 있다.

```javascript
/* 
	구문
	조건: 참 또는 거짓으로 나타낼 수 있는 표현식이다.
	명령문: 해당 조건이 참일 때 실행되는 문이다.
*/
if (조건1) {
    명령문
} else if (조건2) {
	명령문
} else {
    명령문
}
```

* 예시

```javascript
var num = 10;
if (num >= 10) {
    console.log('숫자는 10 이상이다.');
} else if (0 <= num && num < 10) {
    console.log('숫자는 0 이상 10 미만이다');
} else {
    console.log('숫자는 0 미만이다.');
}
// 숫자는 10 이상이다.
```

<br>

####`switch`

* `switch` 문은 표현식 지정하여 표현식의 값을 `case` 절과 일치시키고 해당 케이스와 관련된 명령문을 실행시킨다.
* `default` 표현식과 일치하는 `case`가 없을 때 `default` 절의 명령문이 실행된다.
* `break`를 사용하지 않으면 표현식과 일치한 `case` 절의 명령문을 실행한 후 아래의 `case` 절의 명령문을 모두 실행시키기 때문에 `break` 를 사용해야 한다.

```javascript
/*
	구문
	표현식: case 절과 일치시킬 표현식이다.
	값: 해당 case의 값이다.
	명령문: case 절의 값이 표현식과 일치했을 경우 실행되는 구문이다.
*/
switch (표현식) {
	case 값1 :
        명령문
        break;
    case 값2 :
        명령문
        break;
    default:
        명령문
}
```

* 예시

```javascript
var fruit = 'banana';
switch (fruit) {
    case 'apple':
        console.log('사과는 빨간색');
        break;
    case 'banana':
        console.log('바나나는 노란색');
        break;
    default:
        console.log('사과 또는 바나나를 입력하세요.');
}
// 바나나는 노란색
```

<br>

##반복문

> 자바스크립트 반복문

#### `for`

* `for` 문은 조건을 지정하여 해당 조건이 참일 경우 반복하여 명령문을 실행하는 문이다.

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

* 예시

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

* `while` 문은 조건문이 참일 때 실행되는 반복문이다.

```javascript
/*
	구문
	조건: 매 반복마다 평가할 식이다. 반복이 시작되기 전에 조건을 평가한다.
	명령문: 해당 조건이 참일 때만 실행되는 문이다.
*/
while (조건) {
	명령문
}
```

* 예시

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

####`do... while`

* `do...while` 문은 조건이 거짓으로 평가될 때까지 지정된 구문을 실행하는 반복문이다.
* 단, `do` 구문이 실행된 후 조건이 평가되기 때문에 구문은 무조건 한 번은 실행된다.

```javascript
/*
	구문
	do 구문: 조건이 참일 때마다 한 번이상 실행되는 구문이다.
	while 조건식: 매 반복마다 평가되는 조건식이다. 조건이 거짓이면 do...while문은 종료된다.
*/
do {
    구문
} while (조건식)
```

* 예시

```javascript
var result = '';
var i = 0;
do {
   i += 1;
   result += i + ' ';
}
while (i > 0 && i < 5);

console.log(result);
// 1 2 3 4 5
```

<br>

[🔝 BACK TO TOP](#Table-of-Contents)

<br>

## 이벤트

> 이벤트

<br>

### 이벤트 캡처링

<br>

### 이벤트 버블링



### 이벤트 위임





