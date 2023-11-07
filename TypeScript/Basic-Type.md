# TypeScript 기본 타입
> 타입 스크립트 기본 타입에 대해 알아보자. 이 글은 타입의 의미와 선언 방식에 대해서만 다루고 있으며, 장점 및 단점에 대해서는 언급하지 않는다.
* [Boolean](#boolean)
* [Number](#number)
* [String](#string)
* [Object](#object)
* [Array](#array)
* [Tuple](#tuple)
* [Enum](#enum)
* [any](#any)
* [void](#void)
* null
* undefined
* [never](#never)

## String
> 자바스크립트 변수 타입 문자열인 경우 선언 방법

```ts
let str : string = "Hellow";
```

## Number
> 타입이 숫자인 경우 선언 방법

```ts
let num : number = 10;
```

## Boolean
> 타입이 진위 값인 경우 선언 방법
```ts
let isChecked : boolean = false;
```

## Object
> 타입이 객체인 경우 선언 방법이 다양하다. 정확히 number, string, boolean, bigint, symbol, null, 또는 undefined가 아닌 나머지를 의미한다.

* 객체 리터럴 방식

```ts
const person: { name: string, age: number } = {
    name: "John",
    age: 30
};
```

* 인터페이스를 사용한 객체 선언

```ts
interface Person {
    name: string;
    age: number;
}

const person: Person = {
    name: "John",
    age: 30
};
```

* 타입 별칭 (Type Alias)을 사용한 객체 선언

```ts
type Person = {
    name: string;
    age: number;
};

const person: Person = {
    name: "John",
    age: 30
};
```

* 객체의 일부 속성을 선택적으로 선언
```js
interface Person {
    name: string;
    age?: number; // age 속성은 선택적
}

const person: Person = {
    name: "John"
};
```
=> 선택적이라는 의미는 객체를 생성할때 `age`가 있어도 되고 없어도 된다는 의미이다.

* 동적 속성 이름을 가진 객체 선언

```ts
const obj: { [key: string]: any } = {
    key1: "value1",
    key2: 42
};
```

## Array
> 타입이 배열인 경우 선언 방법

```ts
let arr : number[] = [1,2,3];

// 제네릭도 사용 가능
let arr : Array<number> = [1,2,3];

// 배열 안에 객체가 있는 경우
// 1.
let people: { name: string, age: number }[] = [
    { name: "Alice", age: 30 },
    { name: "Bob", age: 25 },
    { name: "Charlie", age: 35 }
];

// 2. 제네릭도 사용 가능
let people: Array<{ name: string, age: number }> = [
    { name: "Alice", age: 30 },
    { name: "Bob", age: 25 },
    { name: "Charlie", age: 35 }
];
```

## Tuple
> Tuple은 배열의 길이가 고정되고 각 요소의 타입이 지정되어 있는 배열 형식을 의미.

```ts
// 기본적인 튜플 선언
let tuple: [string, number] = ["John", 30];

// 여러 가지 데이터 유형을 가지는 튜플
let mixedTuple: [string, number, boolean] = ["Alice", 25, true];
```

* 튜플의 요소에 대한 접근 방법

```ts
let name: string = tuple[0];  // "John"
let age: number = tuple[1];  // 30
```

만약 정의하지 않은 타입, 인덱스로 접근할 경우 오류가 난다.
```ts
let tuple: [string, number] = ["John", 30];

// 정의하지 않은 인덱스로 접근
let invalidAccess: string = tuple[2]; // Error :  "Element at index 2 is not present in the tuple."

// 타입과 맞지 않는 값을 할당
tuple[1] = "30"; // Error : "Type 'string' is not assignable to type 'number'."
```

## Enum
> 특정 값(상수)들의 집합을 의미.특정 값을 고정하는 또다른 독립된 자료형이라고 보면 된다.

```ts
enum Days {
    Sunday,    // 0
    Monday,    // 1
    Tuesday,   // 2
    Wednesday, // 3
    Thursday,  // 4
    Friday,    // 5
    Saturday   // 6
}
```
```ts
let day : Days = Days.Sunday; // 0
```
enum은 인덱스 번호로도 접근할 수 있다.

```ts
enum Days {
    Sunday,    // 0
    Monday,    // 1
    Tuesday,   // 2
    Wednesday, // 3
    Thursday,  // 4
    Friday,    // 5
    Saturday   // 6
}

let day : Days = Days[0]; 
```
이넘의 인덱스를 사용자 편의로 변경하여 사용할 수도 있다.

```ts
// 직접 인덱스 번호를 지정한다면, 내부적으로 인덱싱이 정해진 숫자 이후로 순차적으로 증가한다고 이해하면 된다.
enum Days {
    Sunday = 2,    // 2
    Monday,        // 3
    Tuesday,       // 4
    Wednesday,     // 5
    Thursday,      // 6
    Friday,        // 7
    Saturday       // 8   
}

let day : Days = Days[2] // Sunday
let day : Days = Days[5] // Wednesday
```

## any
> 단어 의미 그대로 모든 타입에 대해서 허용한다는 의미를 갖고 있다.

```ts
let str: any = 'hi';
let num: any = 10;
let arr: any = ['a', 2, true];
```

## void
> 반환 값이 없는 함수의 반환 타입이다. 아래와 같이 return이 없거나 return이 있더라도 반환하는 값이 없으면 함수의 반환 타입을 void로 지정합니다.

```ts
function printSomething(): void {
  console.log('something');
}

function returnNothing(): void {
  return;
}
```

## Never
> 어떤 종류의 값도 가질 수 없는 타입을 의미. never 타입은 주로 함수가 어떠한 경우에도 반환하지 않거나 예외를 던지는 등의 상황에서 사용된다. 

* 함수가 예외를 던질때
```ts
function throwError(message: string): never {
    throw new Error(message);
}

// 이 함수는 어떠한 값을 반환하지 않고, 예외를 던짐
```

* 무한 루프

```ts
function infiniteLoop(): never {
    while (true) {
        // 무한 루프
    }
}

// 이 함수는 어떠한 값을 반환하지 않고, 무한 루프를 실행한다.
```

#### 참고 자료 
* https://joshua1988.github.io/ts/guide/basic-types.html#%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EA%B8%B0%EB%B3%B8-%ED%83%80%EC%9E%85

* https://inpa.tistory.com/entry/TS-%F0%9F%93%98-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%83%80%EC%9E%85-%EC%84%A0%EC%96%B8-%EC%A2%85%EB%A5%98-%F0%9F%92%AF-%EC%B4%9D%EC%A0%95%EB%A6%AC#%ED%83%80%EC%9E%85_-_never