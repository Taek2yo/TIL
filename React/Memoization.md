# 메모이제이션(Memoization)
> 컴퓨터 프로그램이 동일한 계산을 반복해야 할 때, 이전에 계산한 값을 메모리에 저장함으로써 동일한 계산의 반복 수행을 제거하여 프로그램 실행 속도를 빠르게 하는 기술. 

## React에서의 메모이제이션
* 리액트가 상태관리를 할 수 있는 이유는 가상 DOM을 만들어놓고 값이 바뀔 때 마다 컴포넌트를 새로 그리기 때문이다.

리액트에서는 값을 비교하고 해당 값을 어디서 업데이트해줘야 하는지 찾지 않고 가상 DOM을 새로 그리기 때문에, 값이 그대로인 부분도 매번 새로 그려야 한다는 단점이 있다. 그래서 나온 것이 메모이제이션. 새로 그리는 것을 최소화해 성능을 개선하기 위해 나온 것.

## React에서의 메모이제이션 종류 및 사용법
* 자세한 설명은 제목 클릭
### [React.memo()](/React/React.memo.md)
> props가 같다면 컴포넌트를 새로 그리지 않는다.

#### 사용방법
```js
function StudentInfo({name, age}){
    return(
        <div>
            <span>Student Name : {name}</span>
            <span>Student Age : {age}</span>
        </div>
    )
}

export default React.memo(StudentInfo)
```
위 예제에서, `<StudentInfo>`의 props인 name, age의 값이 변경되지 않는다면 컴포넌트 자체가 리렌더링 되지 않는다.

그렇다면 React.memo에서는 props의 변화를 어떻게 비교할까?

&rarr; **얕은 비교**를 사용한다
> 두 객체가 메모리 상에서 같은 위치를 가리키는 경우에만 두 객체를 동일하다고 판단하는 방식을 사용하기 때문에 객체 안의 값이 같더라도 항상 다른 값으로 판단하게 된다.

만약 `얕은 비교`방식을 사용하지 않고 직접 만들고 싶다면 어떻게 해야할까?

&rarr; `React.memo()`의 두번째 인자로 비교 함수를 만들면 가능하다.

```js
function MemoizedStudent({info}){
    return(
        <div>
            <span>Student name : {info.name}</span>
            <span>Student age : {info.age}</span>
        </div>
    );
}

function propsAreEqual(prev, next){
    return(
        prev.name === next.name && prev.age === next.age
    )
}

export default React.memo(MemoizedStudent, propsAreEqual);
```
* 다만, shallow level에서만 데이터를 비교하므로, 복잡한 구조의 데이터는 비교할 수 없다.


### [useMemo](/React/useMemo.md) 와 [useCallback](/React/useCallback.md)
> 컴포넌트 내부 로직에서 쓰이는 변수, 함수의 재렌더링을 막고자 할 때. (컴포넌트 자체를 새로 그리지 않게하는 React.memo와는 다름)

* 함수형 컴포넌트에서만 쓰인다.
* useMemo : 값을 기억
* useCallback : 함수를 기억

#### 사용방법

```js
const MemoizationTest = useCallback((example) => {
    // 함수 작성
}, [의존성배열]);
```
* `useMemo`, `useCallback` 모두 두번째 인자로 `의존성 배열`을 가지는데, 여기에 속한 변수가 변경될 때 마다 해당 함수가 재렌더링되게 할 수 있다.


#### 참고
[gitHub](https://github.com/uu29/TIL/blob/main/%5BReactJS%5D%20%EB%A9%94%EB%AA%A8%EC%A0%9C%EC%9D%B4%EC%85%98%EC%9C%BC%EB%A1%9C%20%EB%A6%AC%EC%95%A1%ED%8A%B8%20%EC%84%B1%EB%8A%A5%EC%9D%84%20%EC%98%AC%EB%A0%A4%EB%B3%B4%EC%9E%90.md#%EB%A9%94%EB%AA%A8%EC%A0%9C%EC%9D%B4%EC%85%98memozation%EC%9D%B4%EB%9E%80)

https://namu.wiki/w/%EB%A9%94%EB%AA%A8%EC%9D%B4%EC%A0%9C%EC%9D%B4%EC%85%98