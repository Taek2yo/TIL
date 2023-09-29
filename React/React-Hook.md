# 리액트 훅(React Hook) 이란?
훅은 함수형 컴포넌트에서도 상태(state) 관리, 라이프사이클 메서드의 기능을 활용하고 다양한 리액트 기능을 사용할 수 있게 해준다.

함수형 컴포넌트는 클래스 컴포넌트와 달리 더 간결하고 재사용성이 높아지며, 훅을 통해 이러한 컴포넌트에서도 상태 관리 등의 기능을 사용할 수 있게 되었다.

## 규칙

### 1. 훅은 컴포넌트 내부에서만 호출해야 함.
```js
// 좋은 예
function MyComponent() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    // ...
  }, [count]);
  // ...
}

// 나쁜 예
function MyComponent() {
  if (someCondition) {
    const [count, setCount] = useState(0); // 조건문 내에서 호출됨
    // ...
  }
  // ...
}

```

### 2. 훅은 항상 컴포넌트 최상위에서 호출되어야 함
 컴포넌트 함수 내에서 항상 최상위 레벨에서 호출되어야 한다. 즉, 조건문, 반복문, 중첩 함수 내부에서 훅을 호출해서는 안됨.

```js
// 좋은 예
function MyComponent() {
  const [count, setCount] = useState(0);
  if (someCondition) {
    // ...
  }
  // ...
}

// 나쁜 예
function MyComponent() {
  if (someCondition) {
    const [count, setCount] = useState(0); // 조건문 내에서 호출됨
    // ...
  }
  // ...
}
```


### 3. 훅의 호출 순서는 항상 동일해야한다.
컴포넌트 내에서 항상 같은 순서로 호출되어야 한다. 훅의 호출 순서를 변경하면 예상치 못한 동작이 발생할 수 있다.

```js
// 좋은 예
function MyComponent() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    // ...
  }, [count]);
  // ...
}

// 나쁜 예: useState와 useEffect의 호출 순서가 변경됨
function MyComponent() {
  useEffect(() => {
    // ...
  }, [count]);
  const [count, setCount] = useState(0);
  // ...
}
```


### 4. 훅을 조건부로 호출하지 말 것
조건에 따라 훅을 호출하고 싶다면 조건부 렌더링을 사용한다.

```js
// 좋은 예: 조건부 렌더링을 사용하여 조건에 따라 컴포넌트를 렌더링
function MyComponent() {
  if (condition) {
    return <AnotherComponent />;
  }
  return <SomeComponent />;
}
```