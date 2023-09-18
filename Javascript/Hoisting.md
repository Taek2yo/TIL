> ##  🔎	호이스팅이란?

## 호이스팅

👉 함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것

👉 var 변수 선언과 함수선언문에서만 호이스팅이 일어난다.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var 변수/함수의 선언만 위로 끌어 올려지며, 할당은 끌어 올려지지 않는다.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;let/const 변수 선언과 함수표현식에서는 호이스팅이 발생하지 않는다.



## 함수 선언식과 함수표현식

* 함수 선언식 (function declartion)

 👉 함수명이 정의되어 있고, 별도의 할당 명령이 없는 것

```js
function sum(a,b) {
    return a + b;
}
```
* 함수 표현식 (function Expression)

 👉 정의한 function을 별도의 변수에 할당하는 것
 
```js
 const sum = function(a,b) {
    return a + b;
}

```
<br>

## 함수 선언식과 함수표현식의 차이

주요 차이점은, 호이스팅에서 차이가 발생.

* **함수 선언식**은 <span style="color: red">함수 전체</span>를 호이스팅 한다. 정의된 범위의 맨 위로 호이스팅되서 함수 선언 전에 함수를 사용할 수 있다는 것.

* **함수 표현식**은 <span style="color: red">별도의 변수</span>에 할당하게 되는데, 변수는 선언부와 할당부를 나누어 호이스팅 하게 됨. 선언부만 호이스팅하게 된다.

### 예제
함수 선언식 - 정상으로 해당 값 출력

```js
sum(50, 50); // 100
minus(100, 50) // Uncaught TypeError: minus is not a function

function sum(a, b) { // 함수 선언식
  return a + b;
}

var minus = function (a,b) { // 함수 표현식
  return a - b;
}
```
위는 호이스팅이 마치게 되면 다음과 같이 표현할 수 있다.

```js
function sum(a, b) { // 함수 선언식 - 함수 전체 호이스팅
  return a + b;
};

var minus; // 함수표현식 - 선언부만 호이스팅

sum(50, 50); // 100
minus(100, 50) // Uncaught TypeError: minus is not a function

function (a,b) { // 함수 표현식 - 할당부는 그대로
  return a - b;
}
```
아래와 같이, 오류나는 부분, 즉 함수 표현식을 코드를 호출하는 부분 위에 작성하면 에러없이 정상적으로 출력됨. 오류는 나지 않지만, 함수 표현식과 선언식으로 쓰면서 일관성없이 이렇게 작성해야할 필요가 있나 느껴진다.

```js
var minus = function (a,b) { // 함수 표현식
  return a - b;
}

sum(50, 50); // 100
minus(100, 50) // 50

function sum(a, b) { // 함수 선언식
  return a + b;
};
```
함수 선언식으로 작성한 함수는, 함수 전체가 호이스팅 된다고 하였는데, 전역적으로 선언하게 되면, 중복적으로 동명의 함수를 쓰게 된다면, 원치 않는 결과를 초래할 수 있다.

함수 표현식으로 작성하게되면 이를 방지할 수 있다.

#### 출처
* https://taenami.tistory.com/86
* https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html
* https://developer.mozilla.org/ko/docs/Glossary/Hoisting

<br>