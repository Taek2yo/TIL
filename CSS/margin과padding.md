# margin 과 padding의 차이점
> Margin : Object와 화면과의 여백( 요소 외부 여백 ) <br/>
Padding : Object 내의 내부 여백

<div style="dislplay:flex; text-align:center; align-items:center">
<img src="https://velog.velcdn.com/images/hyejin4169/post/5a49d3d5-5fb4-48a9-ac2d-f660d14bbdcf/image.png"/>
</div>

* `Margin`은 Border 바깥쪽을 차지하고, 주변 요소와 거리를 두기 위한 영역이다
<br/> 예를 들어, `button` 요소에 `margin`을 주면 `margin` 영역에는 클릭이 되지 않는다.

* `Padding`은 Content와 Border 사이의 여백을 나타내는 영역이다.
<br/> 예를 들어, `button` 요소에 `padding`을 주면 padding 영역까지도 영향을 미친다. 즉, Content의 연장으로 볼 수 있다.


## 사용법
### margin : top right bottom left
> 시계방향 순서로 값을 준다.

1. 4개 모두 사용
<br/> Ex. `margin : 10px 5px 10px 5px;`

2. 2개 사용
<br/> : 2개의 속성만 사용할 경우, 첫번째 값은 top, right / 두번째 값은 right, left 값을 의미한다
<br/> Ex. `margin : 10px 10px;`

3. 1개 사용
<br/> : 1개만 사용할 경우 4가지 값 모두 같은 값을 사용한다.
<br/> Ex. `margin : 10px ;`

4. padding의 경우 1개만 사용할 경우 안쪽여백이 변경됨.

5. 한가지 속성 부여
<br/> 네 방향 중 하나의 방향에만 값을 부여하고 싶은 경우에, 방향을 지정해주면됨
    > margin-top : 10px; padding-right : 10px ;

6. auto
<br/> margin에만 사용가능하며, 요소의 가로 중앙 정렬을 위해 `margin: 0 auto`와 같이 사용된다.
<br/> padding 에는 auto 속성이 유효하지 않다.