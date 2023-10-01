# useState
> 상태를 관리하는 훅

## 개요
* 함수형 컴포넌트 안에 state를 추가하여 사용한다.
* 현재 상태값 (state) 과 상태를 업데이트하는 함수인 setState를 한 쌍으로 제공한다.
* state는 초기값을 설정할 수 있으며, 초기값은 첫 렌더링 때 한번 사용됨.
* state는 여러가지 다양한 값을 넣을 수 있다.

### 예제
```js
import React, { useState } from "react";

function Example(){
    const [count, setCount] = useState(0);

    const increment = () => {
    setCount(count + 1);
    };
    return(
        <>
        <span> {count} 번 클릭했어요.</span>
        <button  onClick={increment}>
        클릭
        </button>
        </>
    );
}
```

## 특징

### 비동기 업데이트
>  setState 함수는 비동기적으로 상태를 업데이트 한다. 이것은 setState 호출이 즉시 상태를 변경하지 않고, React가 새로운 상태로 컴포넌트를 다시 렌더링할 때까지 대기한다는 것. 때문에 이전 상태에 의존하는 경우 함수를 인자로 전달하는 방식으로 업데이트를 수행하는 것이 좋다.

```js
setCount(prevCount => prevCount + 1);
```

### 이전 상태 값 활용

> 상태 업데이트 시 이전 상태 값을 사용하여 업데이트해야 할 때, 함수를 인자로 사용하여 setCount 함수를 호출하는 것이 중요, 이렇게 할 때에 React가 최신 상태를 보장하며, 예상치 못한 버그를 방지할 수 있다.

```js
const increment = () => {
  setCount(prevCount => prevCount + 1);
};
```

### 복수의 상태 변수
> 함수 컴포넌트에서 여러 개의 상태 변수를 사용할 수 있다. useState를 여러 번 호출하여 다른 상태 변수를 생성하고 관리할 수 있다.

```js
const [number, setNumber] = useState(0);
const [string, setString] = useState("");
```

### 객체 상태
> useState를 사용하여 객체를 상태로 사용할 수 있다. 이는 여러 값을 하나의 상태로 그룹화할 때 유용하다.

```js
const [person, setPerson] = useState({ name: "John", age: 30 });
// 상태 업데이트 시 객체의 일부 속성만 업데이트
setPerson({ ...person, age: 31 });
```

### 함수형 업데이트
> 상태 업데이트 함수를 인자로 받아 함수형 업데이트를 수행할 수 있다. 이전 상태에 의존적인 복잡한 업데이트를 처리할 때 유용하다.

```js
const incrementByTwo = () => {
  setCount(prevCount => prevCount + 2);
};
```