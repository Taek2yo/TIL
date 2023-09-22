# LifeCycle Method
> `생명주기 메서드`. 생명주기 메서드는 컴포넌트가 브라우저상에 나타나고, 업데이트되고, 사라지게 될 때 호출되는 메서드들. 추가적으로 컴포넌트에서 에러가 났을 때 호출되는 메서드도 있다.

> `클래스형 컴포넌트`에서만 사용할 수 있다.

### 컴포넌트에 변화가 발생 할 때마다 생명주기 메서드들을 호출한다.
![라이프사이클](https://github.com/Taek2yo/TIL/assets/110080748/c6af4fb9-fcb8-4010-8bcf-a76ec92a18b9)
출처 : https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/

## 마운트
> 마운트 될 때 발생하는 생명주기들.
* constructor
* getDerivedStateFromProps
* render
* componentDidMount

### constructor
> `constructor`` 는 컴포넌트의 생성자 메서드. 컴포넌트가 만들어지면 가장 먼저 실행

```js
constructor(props) {
    super(props);
    console.log("constructor")
}
```
** `super(props)`는 부모 클래스(이 경우, 현재 클래스의 부모 클래스)의 생성자를 호출하는 키워드. 이렇게 함으로써 부모 클래스의 생성자 코드를 실행할 수 있다.

### getDerivedStateFromProps
> `getDerivedStateFromProps` 는 `props` 로 받아온 것을 `state` 에 넣어주고 싶을 때 사용

```js
static getDerivedStateFromProps(nextProps, prevState) {
    // nextProps로부터 값을 가져와서 상태를 업데이트합니다.
    if (nextProps.newValue !== prevState.value) {
      return { value: nextProps.newValue };
    }
    return null; // 상태를 업데이트하지 않을 경우 null을 반환합니다.
  }
```

* getDerivedStateFromProps 메서드는 React 클래스 컴포넌트의 `정적(static)` 메서드, 컴포넌트의 props에 따라 상태를 업데이트할 수 있다. 

* `null` 또는 `상태를 가진 객체`를 반환하며, 컴포넌트의 초기 렌더링 이전과 이후에 호출된다.

* `this` 사용할 수 없으며, 주로 props의 변화에 따른 상태 조작에 사용된다.

### render
> 컴포넌트를 렌더링하는 메서드


### componentDidMount
>컴포넌트의 첫번째 렌더링이 마치고 나면 호출되는 메서드. 

* 이 메서드가 호출되는 시점에는 컴포넌트가 화면에 나타난 상태.

* 여기에선 DOM 을 사용해야하는 외부 라이브러리 연동을 하거나, 해당 컴포넌트에서 필요로하는 데이터를 요청하기 위해 axios, fetch 등을 통하여 ajax 요청을 하거나, DOM 의 속성을 읽거나 직접 변경하는 작업을 진행한다다.
 

## 업데이트
> 컴포넌트가 업데이트 되는 시점에 호출되는 생명주기 메서드

* getDerivedStateFromProps
* shouldComponentUpdate
* render
* getSnapshotBeforeUpdate
* componentDidUpdate

### getDerivedStateFromProps
> 마운트될 때 뿐만 아니라 컴포넌트의 props 나 state 가 바뀌었을때도 이 메서드가 호출.

### shouldComponentUpdate
> 컴포넌트가 리렌더링 할지 말지를 결정하는 메서드, 주로 최적화 할 때 사용
* 사용법
```js
  shouldComponentUpdate(nextProps, nextState) {
  // 업데이트가 필요한지 여부를 결정하는 조건을 작성
  // true를 반환하면 업데이트가 수행.
  // false를 반환하면 업데이트가 취소.
}
```

* 예제
```js 
 shouldComponentUpdate(nextProps, nextState) {
    // count 상태가 5의 배수일 때만 업데이트를 허용
    if (nextState.count % 5 === 0) {
      return true;
    }
    return false;
  }

  incrementCount = () => {
    this.setState((prevState) => ({
      count: prevState.count + 1
    }));
  }
```

### render
> 위에서 설명했기에, 생략.


### getSnapshotBeforeUpdate
> 컴포넌트가 업데이트된 직후(render 메서드 실행 이후) 호출되는 메서드. 이 메서드는 주로 컴포넌트의 업데이트 전후에 DOM 요소의 상태를 캡처하고 처리하는 데 사용된다.

* 사용법
```js
getSnapshotBeforeUpdate(prevProps, prevState) {
  // DOM 상태를 캡처하거나 다른 데이터를 반환
}
```

* 예제
>  컴포넌트의 업데이트 전후에 스크롤 위치를 캡처하고 업데이트 후에 해당 위치로 스크롤을 복원하는 예제
```js
 componentDidMount() {
    // 초기 데이터 로드 및 스크롤 위치 설정
    // 예: this.setState({ messages: initialMessages, scrollPosition: initialScrollPosition });
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // 스크롤 위치 캡처
    if (prevProps.messages.length < this.props.messages.length) {
      const messagesRef = this.messagesRef.current;
      return messagesRef.scrollHeight - messagesRef.scrollTop;
    }
    return null;
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    // 스크롤 위치 복원
    if (snapshot !== null) {
      const messagesRef = this.messagesRef.current;
      messagesRef.scrollTop = messagesRef.scrollHeight - snapshot;
    }
  }
```

### componentDidUpdate
> componentDidUpdate 는 리렌더링이 마치고, 화면에 원하는 변화가 모두 반영되고 난 뒤 호출되는 메서드. 3번째 파라미터로 getSnapshotBeforeUpdate 에서 반환한 값을 조회할 수 있다.

* 예제 ( 위 예제에서 componentDidUpdate 부분 )

```js
componentDidUpdate(prevProps, prevState, snapshot) {
    // 스크롤 위치 복원
    if (snapshot !== null) {
      const messagesRef = this.messagesRef.current;
      messagesRef.scrollTop = messagesRef.scrollHeight - snapshot;
    }
  }
```


## 언마운트
> 컴포넌트가 화면에서 사라지는 것을 의미. 관련 생명주기 메서드로 `componentWillUnmount` 하나가 있다.

### componentWillUnmount
> 컴포넌트가 화면에서 사라지기 직전에 호출

* 주로 컴포넌트에서 수행한 리소스 해제, 이벤트 처리기 제거 등의 정리 작업을 수행하는 데 사용된다.

* 예제
```js
 componentDidMount() {
    // 컴포넌트가 마운트된 후 3초마다 메시지 업데이트
    this.timer = setInterval(() => {
      this.setState({ message: '째깍째깍...' });
    }, 3000);
  }

  componentWillUnmount() {
    // 컴포넌트가 언마운트되기 전에 타이머 정리
    clearInterval(this.timer);
  }
```

* componentWillUnmount 메서드에서 컴포넌트가 언마운트되기 전에 타이머를 정리한다. 이렇게 하면 컴포넌트가 제거되기 전에 불필요한 리소스 누수를 방지하고 안전한 정리 작업을 수행할 수 있다.


## Error Handling
> `componentDidCatch` 메서드를 사용하여 수행된다. 이 메서드는 컴포넌트 내부에서 발생한 에러를 잡아내고 처리할 수 있는 역할을 한다.

```js
import React, { Component } from 'react';

class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = {
      hasError: false
    };
  }

  componentDidCatch(error, errorInfo) {
    // 에러가 발생했을 때 호출되는 메서드
    console.error('에러가 발생했습니다:', error);
    console.error('에러 정보:', errorInfo);
    this.setState({ hasError: true });
  }

  render() {
    if (this.state.hasError) {
      return <div>에러가 발생했습니다.</div>;
    }
    return this.props.children;
  }
}

class MyComponent extends Component {
  render() {
    if (this.props.showError) {
      throw new Error('컴포넌트에서 발생한 에러');
    }
    return <div>리액트 에러 처리 예제입니다.</div>;
  }
}

class App extends Component {
  state = {
    showError: false
  };

  toggleError = () => {
    this.setState((prevState) => ({ showError: !prevState.showError }));
  };

  render() {
    return (
      <div>
        <h1>리액트 에러 처리 예제</h1>
        <button onClick={this.toggleError}>에러 발생 토글</button>
        <ErrorBoundary>
          <MyComponent showError={this.state.showError} />
        </ErrorBoundary>
      </div>
    );
  }
}

export default App;
```
* 위 예제에서 `ErrorBoundary` 컴포넌트는 `componentDidCatch` 메서드를 구현하여 자식 컴포넌트에서 발생한 에러를 잡아내고, 상태를 업데이트하여 에러 메시지를 화면에 표시한다.


## 정리

### React의 라이프 사이클 ?

" 리액트의 라이프사이클은 컴포넌트의 생성, 업데이트, 소멸과 관련된 단계와 메서드의 집합 "

### 마운트(Mount) 단계

#### constructor 
> 컴포넌트가 생성될 때 호출되는 생성자 메서드로, 초기 설정 및 상태 초기화에 사용된다.

#### render
> 컴포넌트가 렌더링될 때 호출되며, UI를 생성하는 역할을 한다.

####  componentDidMount
> 컴포넌트가 화면에 나타나면 호출되는 메서드로, 초기 데이터 가져오기, 외부 리소스 로드 및 이벤트 구독과 같은 초기화 작업에 적합.

### 업데이트(Update) 단계

#### shouldComponentUpdate 
> 컴포넌트가 업데이트되기 전에 호출되며, 업데이트가 필요한지 여부를 결정하는데 사용된다.

#### render
> 업데이트된 내용을 다시 렌더링.

#### componentDidUpdate
> 컴포넌트가 업데이트를 완료하면 호출되며, 업데이트 이후의 작업에 사용된다.

### 언마운트(Unmount) 단계

#### componentWillUnmount

> 컴포넌트가 화면에서 사라지기 전에 호출되며, 정리 작업에 사용된다. 이벤트 리스너 제거 및 리소스 해제와 같은 작업이 여기에 포함.

### 오류 처리(Error Handling)

#### componentDidCatch

> 컴포넌트 내부에서 에러가 발생하면 호출되며, 에러 처리와 관련된 작업을 수행할 수 있습니다.

<br/>

#### 참고

https://react.vlpt.us/basic/25-lifecycle.html

https://blog.logrocket.com/react-lifecycle-methods-tutorial-examples/