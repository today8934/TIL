# 프록시 패턴(Proxy Pattern)

프록시는 대리자라는 뜻이다.

어떤 객체의 메소드를 호출하려고 할때, 중간에 대리자를 두어 대리자를 통해 원하는 객체의 메소드를 호출하는 방식이다. 실제 호출하는 객체와 대리자는 같은 인터페이스를 구현한다.

- 프록시는 실제 서비스와 같은 이름의 메서드를 구현한다.
- 프록시는 실제 서비스에 대한 참조 변수를 갖는다(Composition)
- 프록시는 실제 서비스의 같은 이름을 가진 메서드를 호출하고 클라이언트에서 반환한다.
- 프록시는 실제 서비스의 메서드 호출 전후에 별도의 로직 수행이 가능하다.

코드로 살펴보자

 

```java
public interface IService {
		String runSomething();
}

public class Service implements IService {
		public String runSomething() {
				return "서비스 짱짱";
		}
}

public class Proxy implements IService {
		IService service;

		public String runSomething () {
				service = new Service();
				return service.runSomething();
		}
}

public class Client {
		public static void main(String[] args) {
				IService proxy = new Proxy();
				proxy.runSomething();
		}
}
```

위 코드에서 클라이언트는 IService 인터페이스를 구현한 Proxy 클래스를 의존하고 있다.  프록시 클래스 내에서 실제 서비스 클래스를 의존하여 클라이언트에서 호출한 것과 같은 이름의 메소드를 반환하기 때문에 클라이언트 입장에서는 실제로 의존하는 서비스에 대해 전혀 모르게 할 수 있다. 또한 실제 서비스를 수행하기 전, 후에 프록시 클래스내에서 다른 로직이 추가될 수도 있다.

또다른 예제를 살펴보자

![https://s3.ap-northeast-2.amazonaws.com/yaboong-blog-static-resources/diagram/proxy-pattern-2.png](https://s3.ap-northeast-2.amazonaws.com/yaboong-blog-static-resources/diagram/proxy-pattern-2.png)

```java
public interface IOder {
		boolean fulfillOrder(Order order);
}
```

```java
public class Warehouse implements IOrder {
		private Hashtable<Integer, Integer> stock;
		private String address;

		@Override
		public void fulfillOrder(Order order) {
				for (Item item : order.getItemList()) {
						Integer sku = item.getSku();
						this.stock.replace(sku, stock.get(sku) - 1);

						processOne();
						processTwo();
						processThree();
				}
		}

		public int currentInventory(Item item) {
				return stock.getOrDefault(stock.get(item.getSku()), 0);
		}
}
```

```java
public class OrderFulfillment implements IOrder {
		private List<Warehouse> warehouses;

		@Override
		public void fulfillOrder(Order order) {
				for (Item item : order.getItemList()) {
						if (warehouse.currentInventory(item) != 0) {
								warehouse.fulfillOrder();
						}
				}
		}
}
```

이 예제는 프록시 패턴이 사용되는 세가지 방법 중 Protection Proxy의 케이스이다. 이는 주체 클래스에 대한 접근을 제어하기 위한 것이다. 프록시 클래스인 OrderFulfillment 클래스에서 재고에 대한 유효성 검증(currentInventory 메소드)까지 수행하므로 주체클래스에서는 재고가 없을 경우에 대한 처리를 신경 쓸 필요가 없게된다.

## 왜 쓰는 걸까?

---

- 인터페이스를 통하여 다형성을 구축할 수 있다.
- 원래의 객체가 하려던 일을 똑같이 수행하면서 그외의 부가적인 작업을 수행할 수 있다(OCP).
- 리소스가 많이 드는 연산을 실제로 필요한 시점에 수행할 수 있다.
- 클라이언트가 실제 객체의 내부 구조를 모르게 할 수 있다.
- 클라이언트는 실제 객체와 동일한 메소드명을 호출하므로 사용성이 좋다.

> [https://yaboong.github.io/design-pattern/2018/10/17/proxy-pattern/](https://yaboong.github.io/design-pattern/2018/10/17/proxy-pattern/)
