# useCallback
> useCallback은 React의 Hook 중 하나로, 함수를 `메모이제이션`하고 불필요한 렌더링을 방지하는 데 사용된다. 주로 이벤트 핸들러 함수나 다른 함수형 프롭스를 최적화하거나, `의존성 배열(dependency array)`을 지정하여 효율적인 리렌더링을 관리할 때 유용하다.

> useCallback 은 특정 함수를 새로 만들지 않고 재사용하고 싶을때 사용한다.

## 특징
### 함수 메모이제이션
> useCallback을 사용하면 함수를 메모이제이션하여, 해당 함수가 동일한 의존성 배열 값일 때 이전에 생성된 함수를 반환한다. 이를 통해 함수를 새로 만들 필요가 없어지며, 성능을 최적화할 수 있다.

### 의존성 배열 설정
> useCallback은 두 번째 인자로 의존성 배열(dependency array)을 받는다. 이 배열에 포함된 값들이 변경될 때만 함수가 다시 생성된다. 의존성 배열을 사용하여 어떤 상태나 프롭스에 의존하는 함수를 최적화할 수 있다.

## 예제
```js
import React, { useState, useCallback } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  // 기본적인 useCallback 사용
  const handleClick = useCallback(() => {
    setCount(count + 1);
  }, [count]); // count가 변경될 때만 함수가 재생성됨

  return (
    <div>
      <p>카운트: {count}</p>
      <button onClick={handleClick}>증가</button>
    </div>
  );
}
```
* 위 예제는 `count` 상태를 의존성 배열에 포함시켜서 `count`가 변경될 때만 함수가 재생성된다. 이렇게 하면 불필요한 리렌더링을 방지할 수 있다.


## 사용시 고려 사항
### 남용하지 말것.
> 성능을 최적화하기 위해 `useCallback`을 모든 함수에 대해 사용하는 것은 성능을 오히려 저하시킬 수 있다. 최적화가 필요한 함수나 의존성이 있는 함수에만 사용할 것.

### 주로 사용하는 곳
> 이벤트 핸들러나 props로 전달되는 콜백 함수에 적합하다.

### React 성능 도구 활용
> useCallback을 사용하여 성능 최적화를 수행할 때, React의 성능 도구(Ex. React DevTools)를 활용하여 컴포넌트 렌더링 및 함수 재생성을 모니터링하면 도움이 된다.