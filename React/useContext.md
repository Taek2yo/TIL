# useContext
> React 컴포넌트에서 Context를 활용하는 훅이다.

## Context는 무엇일까?
> 컨텍스트는 컴포넌트 트리를 통해 데이터를 전파하고, 컴포넌트 간에 상태를 공유할 때 유용한 메커니즘.

### 무슨말일까 ?

컴포넌트 A에서 생성한 데이터( Ex. 사용자 정보, 테마 설정, 언어 설정 등)를 컴포넌트 B, C, D 등 다른 컴포넌트에서 필요로 할 때, 모든 컴포넌트를 일일이 데이터를 전달하는 것이 아니라 Context를 사용하여 `데이터를 공유`할 수 있다는 말이다. 이로써 애플리케이션의 상태와 설정을 쉽게 관리하고 여러 컴포넌트 간에 일관된 데이터를 사용할 수 있게 된다.

`전역 상태 관리 라이브러리`를 사용하지 않고도 React 어플리케이션에서 상태를 공유하고 관리하는 방법 중 하나이다.

간단히 예를 들어보자면, 사용자 로그인 정보를 Context로 전달하면, 다양한 컴포넌트에서 이 정보에 접근하여 로그인 상태에 따라 UI를 조정할 수 있다.

## 예제
> 사용자의 로그인 상태를 컨텍스트로 공유하고 사용자 정보를 읽고 업데이트하는 방법. 

1. 첫째로, Context를 생성한다. 일반적으로 별도의 파일에서 Context를 생성하고 내보냄.
```js
// UserContext.js

import React, { createContext, useContext, useState } from 'react';

// 컨텍스트 생성
const UserContext = createContext();

// 컨텍스트 프로바이더
export function UserProvider({ children }) {
  const [user, setUser] = useState(null);

  return (
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  );
}

// 커스텀 훅으로 사용자 정보에 접근
export function useUser() {
  const context = useContext(UserContext);
  if (!context) {
    throw new Error('UserProvider 내에서 사용해야 합니다.');
  }
  return context;
}

```

2. 다음, 컨텍스트 프로바이더(UserProvider)를 최상위 컴포넌트로 감싸줍니다. 이렇게 하면 하위 컴포넌트에서 useContext를 사용하여 컨텍스트 값을 읽을 수 있다.

```js
// App.js

import React from 'react';
import { UserProvider } from './UserContext';
import UserProfile from './UserProfile';

function App() {
  return (
    <UserProvider>
      <div className="App">
        <h1>사용자 프로필</h1>
        <UserProfile />
      </div>
    </UserProvider>
  );
}

export default App;
```

3. 이제, 아까 생성한 커스텀 훅을 사용해 컨텍스트 값을 읽고 업데이트할 수 있다.

```js
// UserProfile.js

import React from 'react';
import { useUser } from './UserContext';

function UserProfile() {
  const { user, setUser } = useUser();

  const login = () => {
    setUser({ username: 'exampleUser' });
  };

  const logout = () => {
    setUser(null);
  };

  return (
    <div>
      {user ? (
        <div>
          <p>안녕하세요, {user.username}님!</p>
          <button onClick={logout}>로그아웃</button>
        </div>
      ) : (
        <div>
          <p>로그인이 필요합니다.</p>
          <button onClick={login}>로그인</button>
        </div>
      )}
    </div>
  );
}

export default UserProfile;
```

## 정리
기존에 React에서 데이터를 컴포넌트 간에 전달하기 위해서는 기존에는 props를 사용해야 했다. 그러나 컴포넌트 트리가 깊어지면서 데이터를 필요한 모든 컴포넌트에 props로 전달하는 것은 번거로웠고 비효율적이었다. 이런 문제를 해결하기 위해 상태 관리 라이브러리인 Redux와 Mobx 등이 등장했다.

그러나 React 팀은 이러한 문제를 해결하고자 React 버전 16.3부터 Context API를 개선하였다. Context API를 사용하면 단계마다 데이터를 일일이 props로 전달하지 않고도 컴포넌트 트리 전체에 데이터를 제공할 수 있다.

### 참고

https://react.dev/reference/react/useContext

https://www.zerocho.com/category/React/post/5fa63fc6301d080004c4e32b