### Android Touch Flow

Activity안에 FrameLayout안에 View가 하나 있다고 가정해보자.

view에 터치이벤트가 발생했을대 호출되는 메소드의 흐름은 다음과같다.

(해당 메소드에서 로그를 찍는다면 아래와 같은 순서로 로그가 출력될것이다.)



Activity.dispatchTouchEvent()

—— FrameLayout.dispatchTouchEvent()

———— View.dispatchTouchEvent()

———— View.onTouchEvent()

———— View.dispatchTouchEvent()

—— FrameLayout.onTouchEvent()

—— FrameLayout.dispatchTouchEvent()

Activity.onTouchEvent()

Activity.dispatchTouchEvent()



여기서 알수 있는건.. 가장 상위뷰에서 dispatchTouchEvent를 호출하고, 거기서 먼저 자식뷰의 dispatchTouchEvent를 호출한다. 가장 하위뷰에 도달하면 하위뷰부터 onTouchEvent가 발생한다. 이때 onTouchEvent에서 이벤트를 소모하지않고 return false를 하게되면 해당 이벤트는 다시 상위 뷰로 넘겨지게 된다. 그리고 상위뷰의 onTouchEvent가 불리게된다. 결국 아무도 처리하지않으면 최상위 뷰까지 onTouchEvent가 불리게 되는것이다.





