# 클로저(Closure)
> 함수가 속한 렉시컬 스코프를 기억하여, 함수가 렉시컬 스코프 밖에서 실행될 때도 이 스코프에 접근할 수 있게 해주는 기능. 자바스크립트 고유의 개념이 아닌 여러 함수형 프로그래밍 언어에서 공통적으로 발견되는 특성.

## 렉시컬 스코프
> 함수가 선언이 되는 위치에 따라서 상위 스코프가 결정되는 스코프

## 클로저의 핵심은 스코프를 이용해서, 변수의 접근 범위를 닫는(폐쇄)것에 있다

* 외부함수 스코프에서 내부함수 스코프로 접근 불가능하다.
* 내부함수에서는 외부함수 스코프에서 선언된 변수에 접근 기능하다.
* 따라서 내부 함수는 외부함수에 선언된 변수에 접근 가능하다.

## 또 다른 클로저의 개념
내부함수는 외부함수의 지역변수에 접근할 수 있는데 외부함수의 실행이 끝나서 외부함수가 소멸된 이후에도 내부함수가 외부함수의 변수에 접근할 수 있는 것


## 예제1

```js
function foo(){
    const one = 'Hello';
    const two = 'World';

    function greeting(){
        console.log( one + ' ' + two);
    }
    return greeting;
}

const myFunction = foo();
myFunction(); // 'Hello World'
```

* 위 예제에서 `myFunction`이라는 변수는 `foo` 함수를 호출하고 있다. 그래서 `myFunction`을 실행하게 되면 `'Hello World'`가 잘 출력된다. `myFunction`은 변수 `a`와 `b`가 있는 `foo` 함수 스코프 바깥에 있는데 왜 잘 출력이 될까?

> 바로 `클로저` 때문. 모든 자바스크립트 함수는 선언될 당시에 클로저가 형성되어 주변 환경, 즉 렉시컬 스코프를 기억할 수 있게 되는 것.

## 예제2 ( 외부로 전달하는 것이 항상 return을 의미하는 것은 아니다. )

```js
function () {
    var count = 0;
    var button = document.createElement("button");
    button.innerText ="click";
    button.addEventListener("click", function() {
        console.log(++count, "times clicked")
    })
    document.body.appendChild(button)
}

// 별도의 외부객체인 DOM의 메서드(addEventListener)에 등록할 handler함수 내부에서 지역변수를 참조한다.
```
* 지역변수를 참조하는 내부함수를 외부에 전달했기에 클로저는 맞지만, `외부로 전달` 이 항상 return을 의미하는 것은 아니라는 것.


## 주로 사용되는 상황
### 데이터 은닉(Data Encapsulation)
> 클로저를 사용하여 변수와 함수를 캡슐화하고 외부에서 접근을 제한할 수 있다.

```js
function createCounter() {
  var count = 0; // 외부에서 접근 불가능한 변수

  function increment() {
    count++;
  }

  function getCount() {
    return count;
  }

  return {
    increment: increment,
    getCount: getCount
  };
}

var counter = createCounter();
counter.increment();
console.log(counter.getCount()); // 1

```
*  `createCounter` 함수는 `count` 변수와 `increment`, `getCount` 함수를 포함한 객체를 반환합니다. 이로써 `count` 변수가 외부에서 직접 접근되지 않고, `increment`와 `getCount` 함수를 통해 제어된다.

### 콜백 함수(Callback Functions)
> 이벤트 처리나 비동기 작업에서 클로저를 사용하여 상태 정보를 유지하고 콜백 함수에 전달할 수 있다.

```js
function fetchData(url, callback) {
  // 비동기적으로 데이터를 가져온 후 콜백 함수 호출
  setTimeout(function() {
    var data = "데이터 내용";
    callback(data);
  }, 2000);
}

function process(data) {
  console.log("데이터 처리 중: " + data);
}

fetchData("https://example.com/data", process);

```
* `fetchData` 함수는 비동기적으로 데이터를 가져오는 작업을 수행하고, 데이터를 가져온 후 `process` 콜백 함수를 호출합니다. `process` 함수는 클로저를 사용하여 외부 스코프의 데이터에 접근할 수 있습니다.

### 프라이빗 멤버(Private Members)
> 객체 지향 프로그래밍에서 클래스의 프라이빗 멤버를 구현할 때 클로저를 활용할 수 있다.

```js
function Person(name) {
  var privateName = name; // 프라이빗 멤버

  this.getName = function() {
    return privateName;
  };
}

var person = new Person("John");
console.log(person.privateName); // undefined (접근 불가능)
console.log(person.getName()); // "John" (접근 가능)

```
* `Person` 생성자 함수는 `privateName` 변수를 가지고 있으며, 이 변수에 접근하기 위한 메소드인 getName을 제공한다. `privateName`은 외부에서 직접 접근할 수 없으며, `getName` 함수를 통해만 접근할 수 있습니다. 이로써 `privateName`은 프라이빗 멤버로 유지됩니다.
#### 참고

https://hanamon.kr/javascript-%ED%81%B4%EB%A1%9C%EC%A0%80/

https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures

https://blacklobster.tistory.com/7