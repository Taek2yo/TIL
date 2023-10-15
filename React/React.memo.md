# React.memo
> 성능 최적화를 위한 도구 중 하나로 사용되는 함수입니다. 주로 함수형 컴포넌트에서 사용되며, 컴포넌트의 리렌더링을 방지하여 애플리케이션의 성능을 향상시킬 수 있다

다시 말해서, **함수 컴포넌트가 동일한 props로 동일한 결과를 렌더링 해낸다면, React는 컴포넌트를 렌더링하지 않고 마지막으로 렌더링된 결과를 재사용한다**

또한 React.memo는 props 변화에만 영향을 준다. React.memo로 감싸진 함수 컴포넌트 구현에 useState 또는 useContext 훅을 사용한다면, 여전히 state나 context가 변할 때 다시 렌더링된다.
props가 갖는 복잡한 객체에 대하여 **얕은 비교**만을 수행하는 것이 기본 동작이다. 다른 비교 동작을 원한다면, 두 번째 인자로 별도의 비교 함수를 제공하면 된다.

## 왜 사용하는가?
> 불필요한 컴포넌트 렌더링을 방지하여 React 애플리케이션의 성능을 최적화하기 위해 사용된다

### " 참조의 동일성에 의존적인 최적화 "
> 컴포넌트가 실제 데이터 변경이 아니라 단순히 새로운 객체 참조를 받았을 때에도 불필요한 렌더링을 방지하는데 사용된다. 예를 들어, 객체나 배열을 새로 생성하고 그 값을 변경해도, React.memo나 PureComponent 등을 사용하여 동일한 데이터가 전달되면 렌더링을 하지 않는 것을 말한다.


## 사용법
> 고차 컴포넌트이므로 사용 중인 component를 memo로 감싸주기만 하면 된다.

```js
const memoizedComponent = React.memo(
  (props) => (
  /* props를 사용하여 렌더링 */
  (prev, next) => {
  /*
  nextProp가 prevProps와 동일한 값을 가지면 true를 반환하고, 그렇지 않다면 false를 반환
  */
);
```
* 위 예제처럼 memo 내부에 코드를 작성해도 되고, 


```js
function MyComponent(props) {
  /* props를 사용하여 렌더링 */
}
function areEqual(prevProps, nextProps) {
  /*
  nextProp가 prevProps와 동일한 값을 가지면 true를 반환하고, 그렇지 않다면 false를 반환
  */
}
export default React.memo(MyComponent, areEqual);
```

* 위 예제처럼 컴포넌트와 비교 함수를 별도로 작성해서 memo로 감싸 사용해도 된다.

이때 비교 연산으로 들어가는 2번째 인자 예제의 `areEqual` 함수는 동일한가?를 연산하는 함수이므로 props가 동일하면 true를 다르면 false를 반환한다. 즉, React.memo의 비교 함수는 **false인 경우에 리렌더링을 발생시키는 것**이다.

함수명은 변경되어도 상관 없으나, 동일한지 아닌지를 연산하고 동일하지 않을 때 렌더링이 발생한다는 것.

### !! 주의 사항
class 컴포넌트의 `shouldComponentUpdate()` 메서드와 달리, `areEqual` 함수는 props들이 서로 같으면 true를 반환하고, props들이 서로 다르면 false를 반환한다. 이것은 `shouldComponentUpdate`와 정반대의 동작이다.


## 사용하는 경우와 사용하지 말아야 하는 경우

### 사용하는 경우
* 성능 최적화가 필요한 경우
> React.memo를 사용하면 컴포넌트가 동일한 입력(props)를 받을 때 불필요한 리렌더링을 방지할 수 있다. 특히, 렌더링 비용이 높은 컴포넌트나 리스트 아이템과 같이 렌더링이 빈번한 경우에 유용하다.

* 함수 컴포넌트가 순수한(pure) 함수 형태를 갖는 경우
> React.memo는 순수 함수 형태의 컴포넌트에 가장 적합하다. 컴포넌트는 동일한 입력(props)에 대해 항상 동일한 결과를 렌더링해야 한다.


### 사용하지 말아야 하는 경우

* 렌더링이 자주 변해야 하는 경우

> 컴포넌트가 자주 리렌더링되어야 하며, 입력(props)가 빈번하게 변경될 때는 React.memo를 사용하지 않는 것이 나을 수 있다.

* 컴포넌트 자체의 렌더링이 간단한 경우

> 컴포넌트가 렌더링 비용이 낮고 렌더링이 빠르게 수행될 때 React.memo를 사용할 필요가 없을 수 있다.

* 메모이제이션이 필요하지 않은 경우

> 입력 데이터가 자주 변경되지 않고 참조의 동일성에 의존하지 않는 경우 React.memo를 사용할 필요가 없다.

#### 출처 및 참고

https://ko.legacy.reactjs.org/docs/react-api.html#reactmemo

https://velog.io/@yejinh/useCallback%EA%B3%BC-React.Memo%EC%9D%84-%ED%86%B5%ED%95%9C-%EB%A0%8C%EB%8D%94%EB%A7%81-%EC%B5%9C%EC%A0%81%ED%99%94