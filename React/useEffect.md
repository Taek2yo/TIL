# useEffect
>  React 함수 컴포넌트에서 부수 효과(side effects)를 처리하고 생명주기 이벤트를 다루기 위한 훅

## 주요 용도
1. 컴포넌트 마운트 시에 실행할 작업
<br/>: 컴포넌트가 화면에 처음 렌더링될 때 초기화 작업을 수행

2. 특정 상태 또는 props가 변경될 때 실행할 작업
<br/> : 지정된 ```의존성 배열(dependency array)```에 있는 값들이 변경될 때 useEffect 콜백이 다시 실행

3. 컴포넌트 언마운트 시에 실행할 작업
<br/> : 컴포넌트가 화면에서 제거될 때 정리(clean-up) 작업을 수행

## useEffect의 기본 형태
```js
useEffect(() => {
  // side effects를 수행할 코드
  return () => {
    // 정리(clean-up) 코드 (옵션)
  };
}, [dependency1, dependency2, ...]);
```
* 첫 번째 인자로는 부수 효과를 수행하는 함수가 들어가며, 두 번째 인자로는 `의존성 배열(dependency array)`이 들어가고, 의존성 배열에 포함된 값들 중 하나라도 변경될 때마다 부수 효과 함수가 다시 실행된다.


## 예제

```js
import React, { useState, useEffect } from "react";

function Example() {
  const [count, setCount] = useState(0);

  // 컴포넌트 마운트 시에 실행됨
  useEffect(() => {
    console.log("컴포넌트가 마운트됨.");
    return () => {
      console.log("컴포넌트가 언마운트됨.");
    };
  }, []); // 빈 의존성 배열: 컴포넌트 마운트와 언마운트 시에만 실행

  // count 상태가 변경될 때마다 실행됨
  useEffect(() => {
    console.log(`count가 변경됨: ${count}`);
  }, [count]);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <>
      <span>{count} 번 클릭했어요.</span>
      <button onClick={increment}>클릭</button>
    </>
  );
}
```

* 첫 번째 useEffect는 빈 의존성 배열을 가지고 있으므로 컴포넌트가 마운트될 때 한 번 실행되고, 컴포넌트가 언마운트될 때 정리(clean-up) 코드도 실행된다. 

* 두 번째 useEffect는 count 값이 변경될 때마다 실행되며, count 상태가 변경될 때마다 로그가 출력된다.


## 활용 방법 예제

### 데이터 가져오기 및 API 호출
```js
useEffect(() => {
  // API 호출 등의 비동기 작업을 수행
  fetchData();
}, [dependency1, dependency2]);
```
* 의존성 배열 내의 값이 변경될 때마다 데이터를 가져오는 API 호출을 실행할 수 있다.


### 브라우저 이벤트 처리

```js
useEffect(() => {
  const handleClick = (e) => {
    // 이벤트 핸들러 내에서 처리
  };

  window.addEventListener("click", handleClick);

  // 정리(clean-up) 함수
  return () => {
    window.removeEventListener("click", handleClick);
  };
}, []);
```
* 컴포넌트가 마운트될 때 이벤트 리스너를 추가하고, 언마운트 시에 이벤트 리스너를 제거할 수 있다.


### 로컬 스토리지 또는 쿠키 조작
```js
useEffect(() => {
  localStorage.setItem("key", value);

  // 정리(clean-up) 함수
  return () => {
    localStorage.removeItem("key");
  };
}, [value]);
```
* 상태 변수가 변경될 때 로컬 스토리지에 데이터를 저장하고, 언마운트 시에 데이터를 제거가능.


### 타이머와 관련된 작업
```js
useEffect(() => {
  const intervalId = setInterval(() => {
    // 주기적으로 실행되는 작업
  }, 1000);

  // 정리(clean-up) 함수
  return () => {
    clearInterval(intervalId);
  };
}, []);
```
* 타이머를 사용하여 주기적으로 작업을 수행하며, 컴포넌트가 언마운트될 때 타이머를 정리할 수 있다.


## 정리
> useEffect는 컴포넌트의 상태 및 생명주기 이벤트와 관련된 다양한 작업을 처리하기 위한 강력한 도구이다. 의존성 배열을 통해 작업의 트리거를 제어하고, 정리(clean-up) 함수를 사용하여 메모리 누수를 방지할 수 있다.

### 참고
https://react.dev/reference/react/useEffect