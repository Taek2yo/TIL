# useMemo
>  useMemo는 계산 비용이 높은 연산의 결과를 `메모이제이션`하여 렌더링 성능을 최적화하는 데 사용된다. 이 Hook을 사용하면 동일한 입력 값에 대해 동일한 결과를 반환하는 함수나 계산을 최적화할 수 있다.

## 형태
```jsx
const cachedValue = useMemo(calculateValue, dependencies)
```
## 특징

### 메모이제이션
* 메모이제이션이란?
<br/>: 이전에 계산한 값을 메모리에 저장함으로써 동일한 계산의 반복 수행을 제거하여 프로그램 실행 속도를 빠르게 하는 기술
 
> `useMemo`를 사용하여 함수 또는 계산 결과를 메모이제이션한다. 메모이제이션된 결과는 동일한 입력 값이 주어질 때 재계산되지 않고 캐시된 값을 반환한다.

### 의존성 배열
> useMemo는 두 번째 인자로 의존성 배열(dependency array)을 받는다. 의존성 배열에 포함된 값들이 변경될 때만 함수 또는 계산이 다시 실행된다.

## 예제
```js
import React, { useMemo, useState } from 'react';

function Test({ a, b }) {
  // a와 b를 입력으로 받아서 계산 결과를 메모이제이션
  const result = useMemo(() => {
    console.log('계산 중...');
    return a * b;
  }, [a, b]);

  return (
    <div>
      <p>계산 결과: {result}</p>
    </div>
  );
}

function App() {
  const [a, setA] = useState(2);
  const [b, setB] = useState(3);

  return (
    <div>
      <button onClick={() => setA(a + 1)}>A 증가</button>
      <button onClick={() => setB(b + 1)}>B 증가</button>
      <Test a={a} b={b} />
    </div>
  );
}
```
* 위 예제는 `Test` 컴포넌트 내에서 'a'와 'b'를 입력으로 받아서 곱셈을 수행한다. `useMemo`를 사용하여 이 계산 결과를 `메모이제이션`하고, 'a'와 'b'가 변경될 때만 재계산되도록 한다.

## 사용시 고려사항
### 의존성 배열 관리
> 의존하는 값이 변경될 때만 함수나 계산이 다시 실행되므로, 필요한 의존성을 명확하게 해야한다.

### 남용 금지
> 모든 함수나 계산을 메모이제이션 할 경우에, 메모리 소비가 증가되므로 필요한 경우에만 사용한다.

### 성능 최적화시 사용
> 계산 비용이 높은 함수나 계산 결과를 최적화하는데 사용한다. 렌더링 성능을 향상시키기 위해 사용할 수 있다.

#### 참고
https://react.dev/reference/react/useMemo

https://react.vlpt.us/basic/17-useMemo.html