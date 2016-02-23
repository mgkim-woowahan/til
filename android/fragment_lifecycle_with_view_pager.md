## ViewPager에서 Fragment의 생명주기

처음 Fragment생성시 onCreate (딱 한번만 불린다.)

그 후 onCreateViwe->onResume 는 페이지를 이동할때마다 호출.

onPause도 이동하면 호출.

onDestory는 Activity가 종료되면 onCreate된 Fragment  한번에 onDestory

