# var, let, const
> JavaScript에서 변수를 선언하는 데 사용되는 키워드. 각각 변수의 스코프와 할당 가능성에 대해 다른 규칙을 가지고 있다.

## var
* `var` 변수는 함수 외부에서 선언될 때의 스코프는 전역이고, 함수 내에서 선언될 때에는 함수 스코프로 지정된다.

### 예제
```js
var greeter = "hey"

function Test(){
    var hello = "hello"
}

console.log(hello); // error : hello is not defined
```
* `hello`가 함수 스코프, `greeter`는 함수 밖에 존재하므로 전역 스코프를 가진다.
* `hello`가 `Test()` 함수 밖에서는 사용할 수 없으므로 에러가 발생된다.

### var 변수는 재선언, 재할당이 가능하다.

```js
// case 1
var greeter = "hey"
var greeter = "say hello instead"

// case 2
var greeter = "hey"
greeter = "say hello instead"
```
* 같은 스코프(함수 or 전역)내에서라면 `case1`, `case2` 두가지 방법으로 수정이 가능하고 에러가 발생하지 않는다.

### var의 호이스팅

```js
// number 1
console.log(greeter);
var greeter = "say hello";

// number 2
var greeter;
console.log(greeter); // greeter is undefined
greeter = "say hello"
```

* `number 1`과 같이 코드를 작성하면, 자바스크립트는 `number 2`와 같이 해석하기 때문에,
`var` 변수는 스코프 내에서 맨 위로 올려지고, 값은 `undefined`로 초기화된다.

### 문제점
* 위에서 살펴본 것처럼 재선언, 재할당이 가능하다면 문제가 있다. 만약, 의도적으로 재정의한 것이라면 괜찮겠지만, 이전에 선언한 것을 인식하지 못한다면 다른 부분에서 사용했을 때 기대하는 출력결과가 아닌 다른 출력값이 나올 수도 있고, 또한 많은 버그도 발생시킬 수 있다.

=> 그래서 필요하게 된 것이 `let`과 `const`


## let
* `let`으로 선언된 변수는 해당 블록 내에서만 사용가능하다.

```js
let greeting = "say Hi"
let times = 3;

if(times > 2){
    let hello = "say hello instead";
    console.log(hello); // "say hello instead"
}

console.log(hello) // hello is not defined
```
* 중괄호로 감싸진 `hello` 변수가 정의된 블록 외부에서 `hello`를 사용했더니, 에러가 발생했다 === `let` 변수는 블록 스코프이기 때문이다.


### let은 재할당은 가능하지만, 재선언은 불가능하다.
* `var`와 마찬가지로 `let`으로 선언된 변수는 해당 스코프 내에서 재할당이 가능하다. 하지만, `var`와 달리 `let` 변수는 스코프 내에서 다시 선언할 수 없다.

```js
// 에러발생
let greeting = "say Hi";
let greeting = "say Hello instead"; 
// error: Identifier 'greeting' has already been declared
```

```js
// 동일한 변수 선언 , 다른 스코프
let greeting = "say Hi";
if (true) {
    let greeting = "say Hello instead";
    console.log(greeting); // "say Hello instead"
}
console.log(greeting); // "say Hi"
```
* `let`을 사용하는 경우라면, 변수가 스코프 내에서만 존재하기 때문에 이전에 이미 사용한 적이 있는 변수명에 대해서 더 이상 신경쓰지않아도 된다.

### let의 호이스팅

* `var`와 마찬가지로 `let` 선언은 맨 위로 끌어올려진다. `undefined`으로 초기화되는 var와 다르게 `let`의 키워드는 **초기화되지 않는다**. 선언 이전에 `let` 변수를 사용하려고 시도한다면 Reference Error(참조 오류)가 발생할 것.


## const 
* `const`로 선언된 변수는 일정한 **상수** 값을 유지한다.
* `let`과 마찬가지로 `const`선언도 선언된 블록 스코프 내에서만 접근 가능하다.

### const는 재할당, 재선언 모두 불가능하다.

```js
// case 1
const greeting = "say Hi";
greeting = "say Hello instead";// error: Assignment to constant variable.

// case 2
const greeting = "say Hi";
const greeting = "say Hello instead";// error: Identifier 'greeting' has already been declared
```

* `const`로 변수를 선언한 경우에는 위와 같은 두 작업을 수행할 수 없다.
* 그러므로, 모든 `const` 선언은 선언하는 당시에 초기화되어야 한다.
### const 객체는 업데이트할 수 없지만, 객체의 속성은 업데이트할 수 있다.

```js
const greeting = {
    message : "say hi",
    times : 4
}

// 불가능
greeting = {
    words: "Hello",
    number: "five"
} // error:  Assignment to constant variable.


// 가능 
greeting.message = "say Hello instead";
```

### const의 호이스팅
* `const`선언도 맨 위로 끌어올려지지만, 초기화는 되지않는다.


### 결론

* `var`는 전역 스코프 또는 함수 스코프를 가지며, `let`과 `const`는 블록 스코프를 가진다.

* `var` 변수는 스코프 내에서 재할당 및 재선언 가능, `let` 변수는 재할당 가능하지만 재선언 불가능, `const` 변수는 재할당와 재선언 모두 불가능.

* 모든 변수는 최상위로 호이스팅되지만 `var` 변수만 `undefined`로 
초기화되고, `let`과 `const` 변수는 초기화되지 않는다.

* `var`와 `let`은 초기화하지 않은 상태에서 선언할 수 있지만, `const`는 선언과 동시에 초기화해야 한다.


#### 참고
https://www.freecodecamp.org/korean/news/var-let-constyi-caijeomeun/

https://80000coding.oopy.io/e1721710-536f-43f2-823b-663389f5fbfa