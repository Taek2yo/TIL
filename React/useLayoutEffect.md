# useLayoutEffect
> 컴포넌트의 렌더링 직후에 동기적으로 실행되는 효과(Effect)를 생성할 때 사용하는 리액트 훅

## useLayoutEffect 와 useEffect의 주요 차이점

### 1. 실행시점
#### useEffect
> 비동기적으로 실행되며, 컴포넌트의 렌더링이 완료된 후 실행된다. 즉, 렌더링 작업 후에 실행되기 때문에 렌더링이 끝난 화면을 사용자에게 보여준 다음 효과를 실행한다. 
#### useLayoutEffect
> 동기적으로 실행되며, 컴포넌트의 렌더링 직후에 실행된다. 즉, 렌더링 작업이 완료되기 전에 실행되므로 렌더링 작업을 차단할 수 있다.


### 2. 렌더링 차단 가능성
#### useEffect
> 비동기적으로 실행되기 때문에 렌더링 작업을 차단하지 않는다. 사용자에게 화면을 먼저 보여주고, 효과는 나중에 실행된다.

#### useLayoutEffect
>동기적으로 실행되므로 렌더링 작업을 차단할 수 있다. 따라서 주의해서 사용해야 하며, 렌더링 작업에 대한 지연을 발생시킬 수 있으므로 성능에 영향을 미칠 수 있다.

## 예제를 통해 알아보기

### useEffect
```js
import { useEffect, useState } from "react";

function Example() {
  const [name, setName] = useState("");
  const [job, setJob] = useState("")
  
  useEffect(() => {
    setName("민택");
    setJob("개발자")
  }, []);
  
  return (
    <>
      <div className="App">{`내 이름은 ${name}이고, 직업은 ${job} 입니다.`}</div>
    </>
  );
}

export default Example;
```

* `useEffect`를 사용한 코드는 다음과 같은 순서로 실행된다.
1. `<div>내 이름은 이고, 직업은 입니다.</div>`을 페인트

2. 이펙트 내부의 `setName`, `setJob` 호출

3. 재렌더링 실행 => `<div>내 이름은 민택이고, 직업은 개발자 입니다.</div>`

<div style="text-align: center; display: flex; flex-direction: column; align-items:center">
<img src="https://github.com/Taek2yo/TIL/assets/110080748/219a474a-c5fb-4436-b80e-3895d04250a9"/>
</div>

* useEffect 내부에 dom 에 영향을 주는 코드가 있을 경우 사용자 입장에서는 화면의 깜빡임을 보게된다.

### useLayoutEffect

```js
import { useLayoutEffect, useState } from "react";

function Example() {
  const [name, setName] = useState("");
  const [job, setJob] = useState("")
  
  useLayoutEffect(() => {
    setName("민택");
    setJob("개발자")
  }, []);
  
  return (
    <>
      <div className="App">{`내 이름은 ${name}이고, 직업은 ${job} 입니다.`}</div>
    </>
  );
}

export default Example;

```
* `useLayoutEffect`는 브라우저가 화면에 DOM을 그리기 전에 이펙트를 수행하는데, 따라서 위 코드의 실행 순서는 아래와 같다.

1. 레이아웃 이펙트 내부의 `setName`, `setJob` 호출
2. `<div>내 이름은 민택이고, 직업은 개발자 입니다.</div>`를 페인트

<div style="text-align: center; display: flex; flex-direction: column; align-items:center">
<img src="https://github.com/Taek2yo/TIL/assets/110080748/73516f04-30fc-4b6e-a951-e85a5c10ecf1" style="width:400px"/>
</div>

* 페인트가 되기전에 실행되기 때문에 dom 을 조작하는 코드가 존재하더라도 사용자는 깜빡임을 경험하지 않는다.

## 결론
> useLayoutEffect 는 동기적으로 실행되고 내부의 코드가 모두 실행된 후 페인팅 작업을 거친다. 따라서 로직이 복잡할 경우 사용자가 레이아웃을 보는데까지 시간이 오래걸린다는 단점이 있어, 기본적으로는 항상 useEffect 만을 사용하는 것을 권장한다.

* 데이터 fetch
* event handler
* state reset

위 3가지 작업 등은 항상 useEffect를 사용하되, 

```js
import { useLayoutEffect, useState } from "react";

function Test(){
    const [value, setValue] = useState(0);
    
    useLayoutEffect(() => {
    if (value === 0) {
      setValue(10 + Math.random() * 200);
    }
  }, [value]);
   console.log('render', value);

  return (
    <button onClick={() => setValue(0)}>
      value: {value}
    </button>
  );
}
```
화면이 깜빡거리는 상황일 때, 예를들어 위와같이 `state`가 존재하며, 해당 `state` 이 조건에 따라 첫 페인팅 시 다르게 렌더링 되어야 할 때는 `useEffect` 사용 시 처음에 0이 보여지고 이후에 리렌더링 되며 화면이 깜빡거려지기 때문에 `useLayoutEffect` 를 사용하는 것이 바람직하다.



#### 출처 및 참고
https://medium.com/@jnso5072/react-useeffect-%EC%99%80-uselayouteffect-%EC%9D%98-%EC%B0%A8%EC%9D%B4%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C-e1a13adf1cd5

https://www.howdy-mj.me/react/useEffect-and-useLayoutEffect

https://merrily-code.tistory.com/46