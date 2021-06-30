# Public class vs class

## Public class와 class의 차이점은 무엇일까?

---

App.java

```java
public class App{
	
}

public class App2{

}
```

해당 자바파일을 컴파일해 보면 

class App2 is public, should be declared in a file named App2.java

라는 에러 메시지를 뱉는다. App2 클래스가 퍼블릭이므로, [App2.java](http://app2.java) 라는 파일에 선언되어야 한다는 소리.

App.java

```java
class App {

}

class App2 {

}
```

문제없이 컴파일된다.

App.java

```java
class App {

}

public class App2 {

}
```

첫번째 예시와 마찬가지로 class App2 is public, should be declared in a file named [App2.java](http://app2.java) 메시지가 출력된다.

App.java

```java
public class App {

}

class App2 {

}
```

잘 컴파일된다.

## 결론

---

자바는 클래스명 앞에 public이라는 접근제어자를 추가하면 해당 파일의 이름과 public class의 이름이 동일해야만 하는 규칙이 있다.

이는 하나의 자바파일에 여러개의 클래스를 작성하는 경우 대표 클래스를 명시하고 파일명과 동일하게 해주는 것이 코드의 가독성에 도움이 된다는 이유때문이라고함!!!!!!!
