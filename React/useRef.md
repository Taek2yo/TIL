# useRef
> JavaScript를 사용할 때에, 특정 DOM을 선택해야하는 상황에서 `getElementById`,`querySelector` 같은 DOM Selector 함수를 사용하지만,
`React`에서는 `ref` 라는 것을 사용한다. 함수형 컴포넌트에서 `ref`를 사용 할 때에는 `useRef`라는 Hook을 사용한다.

>  또한 useRef는 리렌더링 하지 않는다. 컴포넌트의 속성만 조회&수정한다

## DOM 요소에 접근하는 예제
```jsx
import React, { useRef, useEffect } from 'react';

function MyComponent() {
  // useRef를 사용하여 DOM 요소에 접근
  const ref = useRef(null);

  // 컴포넌트가 마운트된 후 실행되는 side effect
  useEffect(() => {
    // ref를 사용하여 DOM 요소에 접근
    ref.current.style.color = 'red';
  }, []);

  return (
    <div>
      <p ref={ref}>이 텍스트는 빨간색입니다.</p>
    </div>
  );
}
```

## 변수 유지 예제
```jsx
import React, { useRef, useState } from 'react';

function Counter() {
  // useRef를 사용하여 변수 유지
  const ref = useRef(0);
  const [count, setCount] = useState(0);

  const increment = () => {
    ref.current += 1;
    setCount(ref.current);
  };

  return (
    <div>
      <p>카운트: {count}</p>
      <button onClick={increment}>증가</button>
    </div>
  );
}
```
* 위 예제에서 `ref`는 컴포넌트의 렌더링 사이에 유지되며, `increment` 함수에서 값을 수정하고 `count` 상태를 업데이트 한다.


## 사용을 지양해야하는 상황

### 컴포넌트의 상태 변경

> `useRef`를 사용하여 컴포넌트의 상태를 변경 하지말것
* 컴포넌트의 라이프 사이클을 무시하고, 가독성과 유지보수성이 떨어지기 때문에.
* 상태 변경은 `useState`나 `useReducer`와 같은 상태 관리 훅을 사용할 것.

### 렌더링에 영향을 주는 데이터 관리
> `useRef`는 리렌더링과 관련 없는 데이터를 저장하는 데 사용되므로, 컴포넌트의 렌더링에 직접적으로 영향을 주지 않아야 한다.

### 컴포넌트 간의 데이터 전달
> React의 주요 원칙 중 하나는 단방향 데이터 흐름이다. `useRef`를 사용하여 데이터를 전달하면, 이 원칙이 어긋나므로 코드의 유지 보수가 어려울 수 있다.

* `useRef` 대신 `props`를 사용하여 데이터를 전달하고, 필요한 경우에 상태 관리 라이브러리(Ex. Redux, Mobx)를 사용해야 한다.


#### 참고
https://react.vlpt.us/basic/10-useRef.html

https://react.dev/reference/react/useRef