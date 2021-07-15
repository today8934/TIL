# 싱글톤 패턴(Singleton Pattern)

## 싱글톤 패턴이란?

---

싱글톤 패턴은 클래스를 한번만 생성하여 메모리에 할당하고 그 메모리에 객체를 만들어 사용하는 디자인 패턴이다.  
인스턴스를 단 한번만 생성할 수 있도록 생성자를 private으로 선언하여 호출을 제한하고 인스턴스를 호출하는 메소드를 통해 최초 생성된 객체를 반환해주 방식이다.

```java
public class Singleton {
		private static Singleton instance = new Singleton();

		private Store(){}

		public static Singleton getInstance() {
				return instance;
		}
}
```

싱글톤은 다양한 방법으로 구현할 수 있다.

## static block 방식

---

```java
public class StaticBlockSingleton {
		private static StaticBlockSingleton instance;

		private StaticBlockSingleton() {}

		static {
				try {
						instance = new StaticBlockSingleton();
				} catch(Exception e) {
						throw new RuntimeException("Create instance fail. err msg = "
																				 + e.getMessage());
				}
		}

		public static StaticBlockSingleton getInstance() {
				return instance;
		}
}
```

static 블록이 클래스가 로딩 될 때 한번만 실행된다는 특성을 이용한 싱글톤이다. 하지만 인스턴스가 사용되는 시점이 아닌 클래스 로딩 시점에 실행된다.

## Lazy init

---

```java
public class LazyInitSingleton {
		private static LazyInitSingleton instance;

		private LazyInitSingleton() {}

		public static LazyInitSingleton getInstance() {
				if(instance == null) {
						instance = new LazyInitSingleton();
				}
				return instance;
		}
}
```

static block 방식에서 개선되어 클래스 로딩 시점이 아닌 인스턴스가 필요하여 getInstance 메소드를 호출하는 시점에 인스턴스가 생성되는 방식이다.

## Thread Safe + Lazy Init

---

```java
public class TSLISingleton {
		private static TSLISingleton instance;

		private TSLISingleton() {}

		public static synchronized TSLISingleton getInstance() {
				if(instance == null) {
						instance = new TSLISingleton();
				}
				return instance;
		}
}
```

Lazy Init방식과 Thread Safe 방식이 결합된 형태이다. Lazy Init 방식으로 멀티쓰레드 환경에서 사용 할 경우 특정 쓰레드가 동시에 getInstance 메소드를 호출했을 때 인스턴스가 두번 생성되는 문제점을 보완한 것이다. 하지만 synchronized가 성능 저하를 유발한다는 단점이 있다.

## Holder

---

```java
public class HolderSingleton {
		private HolderSingleton() {}

		private static class InnerInstanceClass() {
				private static final HolderSingleton instance = new HolderSingleton();
		}

		public static HolderSingleton getInstance() {
				return InnerInstanceClass.instance;
		}
}
```

static inner 클래스는 getInstance 메소드가 호출되기 전까지는 참조되지 않음으로써 Lazy Init의 장점을 가져가고,  static inner 클래스의 인스턴스가 final로 선언되었기 때문에 값이 다시 할당되지 않도록 하여 thread-safe를 확보할 수 있다.

## 왜 사용하는 걸까?

---

- 프로그램 내부에서 어떤 객체가 단 하나만 존재해야 한다.
- 프로그램 내부의 여러 부분에서 이 객체를 공유하며 사용한다.

예를들어, 한 서버가 올라왔다가 내려가기 전까지의 사용자별 로그인 횟수를 카운트하는 클래스를 만들고자 할때, 이 클래스의 인스턴스는 프로그램 전체에서 단 하나의 인스턴스가 카운트를 관리해야 할 것이다. 사용자가 각각 로그인 할 때 마다 새로운 객체를 생성하여 카운트를 관리한다면 같은 사용자가 여러번 로그인 할 때 마다 카운트가 정상적으로 누적되지 않을 것이다. 이같은 상황에서 객체가 프로그램 내부에서 하나만 생성되도록 보장하고 멀티스레드에서 이 객체를 공유하며 동시성 문제를 해결 해 줄 수 있는 것이다.

## 그렇다면 싱글톤은 왜 안티패턴으로 불릴까?

---

안티패턴(anti-pattern)이란 실제 많이 사용되는 패턴이지만 비효율적이거나 비생산적인 패턴을 의미한다. 싱글톤은 디자인 패턴 중 실무에서 매우 많이 쓰이는 패턴이지만 안티패턴으로도 불리곤 한다.

1. 싱글톤 클래스는 생성자가 private 하므로 상속이 불가능하다.
    - 싱글톤은 자기 자신만이 인스턴스를 생성할 수 있도록 생성자를 private으로 제한한다. 하지만 상속을 통해 다형성을 적용하기 위해서는 다른 클래스에 의존을 주입할 수 있도록 기본 생성자가 필요하므로 객체지향의 장점을 적용하기가 힘들다.
2. 서버 환경에서 싱글톤이 1개만 생성됨을 보장하지 못한다.
    - 서버에서 클래스 로더를 어떻게 구성하느냐에 따라 싱글톤 클래스임에도 불구하고 1개 이상의 객체가 만들어질 수 있다. 또한 서버가 이중화, 또는 다중화되어있는 환경일 경우에도 객체가 독립적으로 생성되므로 반드시 인스턴스가 하나만 생성됨을 보장하기 힘들다.
3. 전역상태가 되기때문에 바람직하지 못하다.
    - 싱글톤의 static 메소드로 인해 언제 어디서든 해당 인스턴스를 사용할 수 있으므로 전역 상태가 되기 쉽다. 아무 객체에서나 자유롭게 접근하여 수정이 가능하게되어 이는 권장되지 않는다.
