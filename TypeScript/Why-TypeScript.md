# Why-TypeScript

## 타입스크립트란?
> 자바스크립트에 타입을 부여한 언어. 브라우저에서 실행하려면 파일을 변환해주어야 하는데, 이 과정을 **컴파일(compile)**이라고 한다.

* TypeScript는 컴파일 과정에서 타입을 지정하기 때문에 컴파일 에러를 예방할 수 있을뿐 아니라, 손쉬운 디버깅이 가능해진다.

## 왜 타입스크립트를 써야하는가?
크게 두가지 관점에서 볼 수 있다.
* 에러의 사전 방지
* 코드 가이드 및 자동 완성 ( 개발 생산성 향상 )

### 에러의 사전 방지

```js
// plus.js
function sum(a, b){
    return a + b;
}

sum(10, 20) // 30
sum(10, '20') // 1020
```

```ts
// plus.ts
function sum(a: number, b: number){
    return a + b;
}

sum(10, 20) // 30
sum(10, '20') // Error: 'string' 형식의 인수는 'number' 형식의 매개변수에 할당될 수 없습니다.
```
* VSCode 상에서 다음과 같은 오류를 확인할 수 있다.
> 즉, 타입을 잘못지정하거나 지정하지 않으면 코드가 실행된 후 브라우저에서 오류를 아는 것이 아니라, 코드상에서 오류를 확인할 수 있다.

![ts타입오류](https://github.com/Taek2yo/TIL/assets/110080748/56645791-0d64-41a6-ab18-b940b79859e9)

* 추가로, 출력 결과도 타입을 지정할 수 있다.
```ts
function sum(a: number, b: number): number{
    return a + b;
}
```

### 코드 가이드 및 자동 완성
> 객체 안의 필드값을 다 기억할 필요 없이 IDE가 자동으로 리스트 업을 해주기 때문에 생산성에도 큰 기여를 한다. API도 마찬가지.

```js
// math.js
function sum(a, b) {
  return a + b;
}

let total =  sum(10, 20);
total.toLocaleString();
```

* 위의 예제에서 `toLocaleString()`이라는 API의 역할이 중요한 것이 아니고, `total` 이라는 변수의 타입이 코드 작성 시점에 `number`라는 것을 자바스크립트가 인지하지 못하고 있는 것이 중요하다.

> 즉 , 개발자가 스스로 `sum()`함수의 결과를 가정하고 코딩하게 되는 것. 오류를 발생 시킬 수 있는 가능성이 있다( 오탈자 등 ). 또한 브라우저에서 실행했을 때만 오류를 확인할 수 있을 것.


```ts
function sum(a: number, b: number): number {
  return a + b;
}
let total = sum(10, 20);
total.toLocaleString();
```
![tsAPI](https://github.com/Taek2yo/TIL/assets/110080748/64b0158e-9eb4-4d99-abed-675da7889727)

* 반면에 위의 TS 예제에서는,  IDE가 API를 자동으로 리스트 업해준다.


#### 참고 자료
https://www.elancer.co.kr/blog/view?seq=183

https://joshua1988.github.io/ts/why-ts.html#%EC%99%9C-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%A5%BC-%EC%8D%A8%EC%95%BC%ED%95%A0%EA%B9%8C%EC%9A%94