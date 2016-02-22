# Android Gradle Tip

### build.gradle에서 쓰이는 변수 관리하기

만약 많은 안드로이드 모듈들을 사용하고 있다면, 각 모듈마다 직접 값을 입력하는 일은 피하고 싶을거다.

root project의 build.gradle에 다음과 같이 추가하면 안드로이드 모듈에서 사용가능하다



**루트프로젝트의 build.grade 에서 선언 **

``` groovy
ext {
  complieSdkVersion = 19
  buildToolsVersion = "19.0.1"
}
```

**모듈의 build.grade  에서 사용**

``` groovy
android {
  compileSdkVersion rootProject.ext.compileSdkVersion
  buildToolsVersion rootProject.ext.buildToolsVersion
}
```



이렇게 하면 단한번만 build.grade 를 업데이트 해주면 된다.













참고 : http://tools.android.com/tech-docs/new-build-system/tips