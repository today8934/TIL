# StringBuffer vs StringBuilder

## String은 불변(Immutable)

---

```java
String str = "Hello";
str+= " World";
```

위 코드가 실행되면 처음 Hello값을 가진 str객체의 주소에 World를 더해 Hello World를 갖게 된다고 생각되지만 String 클래스는 처음의 Hello를 가지고있는 주소는 내버려두고 Hello World를 가진 새로운 메모리 주소를 할당한다.  기존의 Hello값을 가진 인스턴스는 가비지로 남아있다가 가비지 컬렉터에 의해 제거되게 된다.

***String 클래스는 불변(Immutable) 하기 때문에 World값을 더했을 때 Hello World값을 가진 새로운 String 인스턴스를 생성한다.***

String은 위와 같이 불변성을 가지기 때문에 자주 변하지 않는 값을 가질때 사용해 주면 좋은 성능을 이끌어 낼 수 있다. 하지만 추가, 수정, 삭제 등의 변화가 빈번한 경우라면 메모리의 Heap영역에 많은 가비지가 생성되게 되어 프로그램의 성능에 안좋은 영향을 끼칠 수 있다.

## 가변성(Mutable)을 가지는 StringBuffer와 StringBuilder

---

위와 같은 문제를 해결하기 위해 Java에서는 가변성을 가지는 StringBuffer와 StringBuilder 클래스를 도입했다. StringBuffer와 StringBuilder 에서는 동일 인스턴스 내에서 append()나 delete() 등으로 문자열을 수정하는것이 가능하다. 그러므로 수정이 빈번한 문자열을 사용해야 할 경우 StringBuffer와 StringBuilder 클래스를 사용하는 것이 용이하다.

## StringBuffer와 StringBuilder의 차이점은?

---

동일하게 append와 delete를 할 수 있는 두 클래스 이지만 차이점은 무엇일까?

가장 큰 차이점은 동기화 유무로써 StringBuffer는 동기화를 지원하여 **멀티쓰레드 환경에서 안전하다는 점(thread-safe) 이다**.  참고로 String도 ****불변성을 가지기때문에 마찬가지로  **멀티쓰레드 환경에서의 안정성(thread-safe)**을 가지고 있다.

반대로 **StringBuilder**는 **동기화를 지원하지 않기**때문에 멀티쓰레드 환경에서 사용하는 것은 적합하지 않지만 동기화를 고려하지 않는 만큼 **단일쓰레드에서의 성능은 StringBuffer 보다 뛰어나다**.

<img src="https://t1.daumcdn.net/cfile/tistory/99BE23375E2F133722">
