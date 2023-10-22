# Button의 type 속성
> button 요소가 클릭 가능한지 여부와 어떻게 동작하는지를 정의하는데 사용된다.

* submit, button, reset 3종류가 있고, defaul 값은 `submit`이다.

* 어떤 이유로 특정 영역을 form 태그로 감싸게 된다면, 그 안에 있던 타입 명시 없는 버튼은 모두 `submit` 버튼으로 동작한다. 

* button 태그를 form 태그 외부에서 사용할 때에는 type이 `submit`이어도 동작하지 않지만, 웹 접근성을 고려할 때 단순 버튼은 type="button"으로 명시하는 것이 좋다.


## input type="button"

* button 태그는 html4에서 등장했는데, button 태그 등장 이전에 button의 동작을 input type="button"을 이용해 대신했다.

* input 태그는 닫힌 태그라 자식을 가질 수가 없지만, button은 자식 태그를 가질 수 있고, CSS에서 가상 선택자로 꾸며주는 것도 가능하다.

### 비교 예제

```html
<form>
  <input type="submit" value="버튼" />
</form>
```

```html
<form>
  <button>
    <img src="images/button.png" alt/>
    <span>멋있는 버튼</span>
  </button>
</form>
```