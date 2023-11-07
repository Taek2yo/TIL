# props & state
> 둘 다 일반 자바스크립트 객체이며, state는 컴포넌트 내부에서만 사용되고 props는 컴포넌트에 매개변수 처럼 전달하는 것.

## props ( properties )

*  부모 컴포넌트가 자식 컴포넌트에 데이터를 전달하는 데 사용된다.

*  불변(immutable, 읽기전용)이며, 자식 컴포넌트에서 수정할 수 없다.

```jsx
function ParentComponent() {
  return <ChildComponent name="John" age={30} />;
}

function ChildComponent(props) {
  return (
    <div>
      <p>Name: {props.name}</p>
      <p>Age: {props.age}</p>
    </div>
  );
}
```

### 모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 한다.
 React 공식 문서에는 이렇게 나와있다. 그렇다면 순수 함수는 뭘까? 바로, **항상 동일한 입력값에 대해 동일한 결과를 반환하는 함수**이다.

### 왜 그래야하는데?
`props`는 본질적으로 컴포넌트 외부에서 전달되는 데이터이며, 컴포넌트 자체에서 수정하거나 변경해서는 안되기 때문이다. 또한 공식문서에서는 `state`도 불변한 것처럼 다루는 것을 권장하고 있다.


## state

* 컴포넌트 내부에서 관리되는 변경 가능한 데이터

*  state는 클래스형 컴포넌트에서 `this.state` 객체를 통해 사용할 수 있으며, `setState()`를 사용하여 변경할 수 있다.

> `state`는 변경 가능한 데이터 이지만, 위에서 공식문서에서도 `state`를 불변한 것처럼 다루는 것을 권장하고 있다고 했다. 그 이유는 무엇일까 ?

`state`를 직접 수정하면 React의 상태 관리를 우회하게 되어, 이는 잠재적으로 위험한 상황을 초래할 수 있다.

예를 들어, `this.state`를 직접 변경하면 React가 이 변경을 감지하지 못하고, 컴포넌트를 다시 렌더링할 필요가 없다고 잘못 판단할 수 있다. 그러나 이후에 `setState()`를 호출하면 이전의 상태 변경이 무효화될 수 있다.

React는 `state`의 변경을 추적하고, `setState()`` 메서드를 통해만 상태를 변경할 때 적절한 렌더링과 업데이트를 수행하도록 설계되어있다. 그러므로 직접 상태를 수정하면 React의 이러한 메커니즘을 우회하게 되어, 예기치 않은 결과를 초래할 수 있다.


### 그렇다면, 이런 불변성은 어떻게 유지할 수 있을까?
> state를 업데이트 할 때, 값은 같아도 새로운 참조 값을 가진 객체를 전달하는 여러 방식을 사용할 수 있다.

#### 1. Spread 연산자 (객체 및 배열)

```jsx
import React, { useState } from 'react';

const ExampleComponent = () => {
  const [person, setPerson] = useState({ name: 'John', age: 30 });

  const changeName = (newName) => {
    // Spread 연산자를 사용하여 객체를 복사하고 변경사항만 추가.
    setPerson(prevPerson => ({ ...prevPerson, name: newName }));
  };

  return (
    <div>
      <p>이름 : {person.name}</p>
      <p>나이 : {person.age}</p>
      <button onClick={() => changeName('Alice')}>
        이름 변경
      </button>
    </div>
  );
};

export default ExampleComponent;
```

#### 2. 객체 비구조화 할당(Destructuring Assignment)

```jsx
import React, { useState } from 'react';

const ExampleComponent = () => {
  const [person, setPerson] = useState({ name: 'John', age: 30 });

  // 객체 비구조화 할당을 사용하여 상태로부터 원하는 값들을 추출.
  const { name, age } = person;

  const changeName = () => {
    // 객체 비구조화 할당을 사용하여 이름을 추출하고 업데이트.
    setPerson(prevPerson => ({ ...prevPerson, name: 'Alice' }));
  };

  return (
    <div>
      <p>Name: {name}</p>
      <p>Age: {age}</p>
      <button onClick={changeName}>
        Change Name
      </button>
    </div>
  );
};

export default ExampleComponent;
```


## 자식 컴포넌트에서 부모 컴포넌트로 데이터 전달 방법
> React는 단방향 바인딩이기 때문에, props는 부모 컴포넌트에서 자식 컴포넌트로만 넘겨 줄 수 있다.

### 정말 안되는걸까?
아니다. 방법은 있다. `props`로 부모 컴포넌트의 상태를 변경하는 함수를 전달하고, 자식 컴포넌트에서 `props`로 넘겨받은 함수를 호출해서 부모 컴포넌트의 상태를 변경할 수 있다.

```jsx
import React, { useState } from 'react';

function ParentComponent() {
  const [counter, setCounter] = useState(0);

  // 자식 컴포넌트에서 호출할 함수
  const updateCounter = (newCounter) => {
    setCounter(newCounter);
  };

  return (
    <div>
      <p>Counter: {counter}</p>
      {/* 자식 컴포넌트를 렌더링하고 함수를 전달 */}
      <ChildComponent onUpdateCounter={updateCounter} counter={counter} />
    </div>
  );
}

function ChildComponent(props) {
  // 버튼을 클릭할 때 카운터 값을 증가시키고 부모 컴포넌트의 함수를 호출
  const handleButtonClick = () => {
    props.onUpdateCounter(props.counter + 1);
  };

  return (
    <div>
      <button onClick={handleButtonClick}>카운터 증가</button>
    </div>
  );
}

export default ParentComponent;
```

## 결론
`props`는 부모 컴포넌트로부터 전달되는 불변한 데이터로, 자식 컴포넌트에 매개변수처럼 전달되며, 변경할 수 없습니다. 반면 `state`는 컴포넌트 내부에서 관리되는 변경 가능한 데이터로, `setState()`를 사용하여 업데이트할 수 있지만, 불변성을 유지하는 것이 권장된다.

또한, 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하려면 `props`를 사용하며, 콜백 함수를 전달해 부모 컴포넌트의 상태를 변경해보았다.

React의 단방향 데이터 흐름 및 불변성 원칙을 따르면 효율적인 React 개발이 되지않을까?


#### 참고자료

[props](https://ko.legacy.reactjs.org/docs/components-and-props.html)

[state](https://ko.legacy.reactjs.org/docs/faq-state.html)

[prop vs state](https://github.com/uberVU/react-guide/blob/master/props-vs-state.md)