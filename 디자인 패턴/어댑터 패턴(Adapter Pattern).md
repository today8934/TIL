# 어댑터 패턴(Adapter Pattern)

## 어댑터 패턴

---

어댑터 패턴은 말그대로 콘센트의 어댑터 처럼 사용되는 패턴이다. 흔히 하는 표현으로, 한국에서 사용하던 200v 콘센트의 전자제품을 110v를 사용하는 미국이나 일본같은 해외에 나가 사용할 때, 220v 콘센트를 110v 콘센트에 사용할 수 있도록 어댑터를 사용한다.

자바의 어댑터 패턴은 이와 마찬가지로 호환성이 없는 인터페이스 때문에 함께 사용할 수 없는 클래스들을 어댑터 패턴을 통해 함께 사용할 수 있도록 해준다.

<img src="https://t1.daumcdn.net/cfile/tistory/99AAB74D5C305D4721">

역시 코드로 봐야 이해가됨. 위 그림을 코드를 짜보자

```java
public class Client{
		public static void main(String[] args) {
				Target process = new OldRequest();
				process.request();
		}
}

public interface Target {
		void request();
}

public class OldRequest implements Target {
		@Override
		public void request() {
				System.out.println("이건 원래 쓰던것이다!!!");
		}
}
```

해당 로직을 사용하고 있는 상황에서 

```java
public class NewRequest {
		public void awesomeNewRequest() {
				System.out.println("새로운 짱짱맨로직");
		}
}
```

해당 클래스를 사용하려고 하는 상황이다. 예제 코드는 매우 짧은 코드이기에 쉽게 클라이언트를 수정이 가능하지만, 매우 복잡한 실무 소스라면 클라이언트 코드의 매우 많은 부분의 수정이 불가피하다. 이러한 상황에서 어댑터 패턴을 통해 클라이언트 소스의 수정없이 사용하려 한다.

```java
public class Adapter implements Target {
		private NewRequest newRequest;

		public Adapter(NewRequest newRequest) {
				this.newRequest = newRequest;
		{

		@Override
		public void request() {
				newRequest.awesomeNewRequest();
		}
}			
```

이렇게 어댑터 클래스를 통해 Target을 구현하여 클라이언트에서는 의존만 기존 클래스에서 어댑터로 교체해주면 된다.
