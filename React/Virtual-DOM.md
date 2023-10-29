# Virtual DOM

## DOM 이란
> 하나하나의 Element(HTML)들을 담고 있는 웹페이지를 Document라고 하는데, 브라우저가 이를 분석해 페이지를 띄워주는 방식. DOM이란 HTML element들을 tree형태로 표현한 것

<div style="dislplay:flex; text-align:center; align-items:center">
<img src="https://www.tcpschool.com/lectures/img_js_htmldom.png"/>
</div>

* `DOM tree`안에는 각각의 element에 상응하는 `Node`가 들어있는데, 개발자들은 DOM이 제공하는 API를 통해서 DOM을 조작할 수 있다. 예를 들어 `getElementById`, `querySelector` 등 API를 이용해 돔 구조안의 Element에 접근해 원하는 대로 조작할 수 있다는 것.

## Virtual DOM
> 메모리에 존재하는 가짜 또는 가상의 DOM 트리. 실제 DOM과 동기화되지 않으며, 실제 DOM의 복사본으로 간주된다.

* 차이점 : 브라우저에 있는 문서에 직접적으로 접근할 수 없기 때문에, 화면에 보여지는 내용을 직접 수정할 수 없다는 것.

## Virtual DOM 사용 이유
> 직접 수정할 수도 없는데 Virtual DOM을 왜 사용할까 ?

* Virtual DOM은 실제 DOM과 내용을 공유하는 복사본이다. 그리고 실제 DOM과 다르게 브라우저 화면의 UI를 조작할 수 있게 하는 API는 제공하지 않는다. 왜냐하면 가상돔은 메모리에 저장되어 있는 자바스크립트 객체에 불과하기 때문에, 가상돔에 접근하는 것은 매우 가볍고 빠른 작업이 되는 것. - `실제 브라우저에 접근하는 것이 아니기 때문에!`


## React의 Virtual DOM 활용
> 리액트는 두개의 Virtual DOM 객체를 사용한다.

1. 렌더링 이전 화면 구조를 나타내는 Virtual DOM
2. 렌더링 이후 보이게 될 화면 구조를 나타내는 Virtual DOM

<div style="dislplay:flex; text-align:center; align-items:center">
<img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*JCrDk-N-wpPnE9j0GObItg.png"/>
</div>


* 리액트는 상태(state)가 변경될 때마다 리렌더링을 수행하며, 이 과정에서 새로운 내용이 담긴 Virtual DOM을 생성한다.

리액트는 Diffing 알고리즘을 사용하여 두 가상 DOM을 비교하여 어떤 엘리먼트가 변경되었는지 파악하는데, 이를 통해 차이가 발생한 부분만을 실제 DOM에 적용하게 되는 것.

이를 `Reconciliation` 이라고 한다. 이 과정이 효율적인 이유는 `Batch Update`를 사용하기 때문인데, `Batch Update`는 변경된 엘리먼트를 한 번에 실제 DOM에 적용하는 방식으로, 여러 엘리먼트의 변경이 동시에 반영되어 브라우저에 화면을 한 번에 그려주는 효율적인 방식이다.

이를 통해 DOM 조작 비용을 최소화하고 성능을 향상시키며, 변경된 엘리먼트를 효율적으로 브라우저에 적용할 수 있게 되는것이다.



#### 출처 및 참고

https://callmedevmomo.medium.com/virtual-dom-react-%ED%95%B5%EC%8B%AC%EC%A0%95%EB%A6%AC-bfbfcecc4fbb

https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction

https://www.tcpschool.com/javascript/js_dom_concept