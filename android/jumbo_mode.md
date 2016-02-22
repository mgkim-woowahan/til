## JumboMode

#### Java 진영

java코드를 컴파일하면 *.class파일이 생성된다. 이 *.class 파일은 JVM에서 동작하는 java bytecode를 가지고있다.

#### Android 진영

안드로이드는 Java와는 다르다. 물론 Java 언어를 이용해 코드를 작성하지만, 컴파일러는 *.class파일을 생성하는 대신 *.dex file을 생성한다. *.dex 파일은 Android Virtual Machine인 dalvik에서 동작한다. (당연히 JVM에선 동작 안한다.)

즉, dex  파일은 JVM에서의 class 파일과 동일하다고 보면 된다.



dexoptions는 java 코드를 android byte 코드로 변경할때 사용되는 설정이다. 

jumboMode는 dex 파일에 많은 string이 들어갈 수 있게 하는 옵션이다.