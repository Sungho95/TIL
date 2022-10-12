![IoC.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/02342824-4da2-4e2b-bd5a-f814b8e01fd0/IoC.png)

## IoC(Inversion of Control)란?

![IoC2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/54c68579-c920-496d-ba04-6222f4deb54e/IoC2.png)

프레임워크와 라이브러리의 가장 큰 차이는 해당 애플리케이션의 흐름의 제어권(주도권)에 있다.

라이브러리는 애플리케이션 흐름의 주도권이 개발자에게 있고, 프레임워크는 애플리케이션 흐름의 주도권이 프레임워크에 있다.

IoC(제어의 역전 또는 제어의 역행)는 애플리케이션 흐름의 주도권이 뒤바뀐 것을 뜻한다.

IoC는 개발자가 프레임워크 API를 사용하면서 설정 파일을 통해 객체의 생명주기, 클래스 등을 프레임워크가 직접 제어권을 갖게 되었다. 이처럼 개발자의 제어권이 프레임워크로 넘어가게 되어 제어의 역전이라 부른다.

IoC는 제어의 역전 또는 제어의 역행이라 불리며 스프링의 가장 핵심적인 기능으로 객체의 생명주기를 관리하고 의존성 주입(DI)을 통해 각 계층이나 서비스들간의 의존성을 맞춰준다.

## Java 콘솔 애플리케이션의 일반적인 제어권

```java
public class printHello {
	public static void main(String[] args) {
		System.out.println("Hello IoC");
	}
}
```

위 코드와 같이 Java 콘솔 애플리케이션을 실행하려면 main() 메서드가 있어야 한다.

main() 메서드를 통해 다른 객체의 메서드나 로직을 실행하기 때문이다.

이와 같이 개발자가 작성한 코드를 순차적으로 실행하는 것이 애플리케이션의 일반적인 제어 흐름이다.

## Java 웹 애플리케이션에서 IoC가 적용되는 예

Java 콘솔 애플리케이션이 아닌 웹에서 돌아가는 Java 웹 애플리케이션의 경우에는 서블릿 기반의 애플리케이션을 웹에서 실행하기 위한 서블릿 컨테이너의 모습이다.

![IoC3.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4e6f8235-59a6-41fd-b93a-c47fe5ad0d34/IoC3.png)

Java 콘솔 애플리케이션의 경우 main() 메서드가 종료되면 애플리케이션의 실행이 종료된다.

하지만, 웹에서 동작하는 애플리케이션은 클라이언트가 외부에서 접속하여 사용하는 서비스이기 때문에 main() 메서드가 종료되지 않아야 한다.

하지만 서블릿 컨테이너에는 서블릿 사양(Specification)에 맞게 작성된 서블릿 클래스만 존재하며 별도의 main() 메서드가 존재하지는 않는다.

main() 메서드처럼 애플리케이션이 시작되는 지점을 엔트리 포인트(Entry point)라 부른다.

서블릿 컨테이너의 경우 클라이언트의 요청이 들어올 때마다 서블릿 컨테이너 내의 로직(service() 메서드)이 서블릿을 직접 실행시켜 주기 때문에 main() 메서드가 필요 없다.

이러한 경우 서블릿 컨테이너가 서블릿을 제어하고 있기 때문에 애플리케이션의 주도권은 서블릿 컨테이너에 있다. 즉, 서블릿과 웹 어플리케이션 간에 IoC(제어의 역전)의 개념이 적용되어 있는 것이다.

Spring에서는 IoC 개념을 적용시키기 위해 DI(Dependency Injection, 의존성 주입)를 사용한다.

## DI(Dependency Injection)란?

![IoC4.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e6493614-5888-4c24-94d9-c7e6fcb09aaf/IoC4.png)

IoC(Inversion of Control)는 서버 컨테이너 기술, 디자인 패턴, 객체 지향 설계 등에 적용하게 되는 일반적인 개념이다.

DI(Dependency Injection)는 IoC 개념을 구체화 시킨 것으로 해석할 수 있다.

DI를 직역하여 의존성 주입이라고도 하며, 객체지향 프로그래밍에서 객체간의 의존 관계를 느슨하게 해주는 것이다.

**의존성?**

만약, A와 B라는 두 개의 클래스 파일이 존재할 때,

A 클래스에서 B 클래스의 기능을 사용하기 위해 B 클래스에 구현되어 있는 어떤 메서드를 호출하는 상황이 있다면, A 클래스는 B 클래스에 의존하게 된다.

![DI.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/58789a15-be20-4cf9-a01f-44438bb7637f/DI.png)

위 그림은 A 클래스가 B 클래스의 기능을 사용하는 것을 다이어그램으로 표현한 것이다.

해당 그림처럼 A 클래스가 B 클래스의 기능을 사용할 때, A 클래스는 B 클래스에 의존한다고 표현한다.

이를 코드로 표현하면 다음과 같이 나타낼 수 있다.

MenuController 클래스

```java
public class MenuController {
	public static void main(String[] args) {
		MenuService menuService = new MenuService();
		List<Menu> menuList = menuService.getMenuList();
	}
}
```

MenuService 클래스

```java
public class MenuService {
	public List<Menu> getMenuList() {
		return null;
	}
}
```

다음과 같이 MenuController 클래스(A) 코드와 MenuService 클래스(B) 코드가 있다.

MenuController 클래스에서는 MenuService 클래스의 객체를 선언하고, MenuService 클래스 내에 구현되어 있는 getMenuList() 메서드를 사용하고 있다.

이러한 경우 MenuController 클래스(A)는 MenuService 클래스(B)에 의존한다고 표현한다.

MenuController 클래스는 클라이언트의 요청을 받는 엔드포인트(Endpoint) 역할을 하고, MenuService 클래스는 MenuController 클래스가 전달 받은 클라이언트의 요청을 처리하는 역할을 한다.

MenuController 클래스는 new 연산자를 통해 MenuService의 클래스 객체를 생성한 후 getMenuList() 메서드를 호출하는 것이다.

이처럼 클래스 간에 사용하고자 하는 클래스의 **객체를 생성해서 참조하게 되면 의존 관계가 성립**하게 된다.

엔드포인트(Endpoint) : 클라이언트가 서버의 자원(리소스)을 이용하기 위한 끝 지점

## **DI(의존성 주입)**

MenuController 클래스와 MenuService 클래스는 의존 관계가 성립되었지만 DI(의존성 주입)는 이루어지지 않았다.

**Client 클래스**

```java
public class Client {
	public static void main(String[] args) {
		MenuService menuService = new MenuService();
		MenuController controller = new MenuController(menuService); // 의존성 주입
		List<Menu> menuList = controller.getMenus();
	}
}
```

**MenuController 클래스**

```java
public class MenuController {
	private MenuService = menuService;
	
	// 생성자의 파라미터를 MenuService의 객체로 입력받음
	public MenuController(MenuService menuService) { 
		this.menuService = menuService;
	}

	public List<Menu> getMenus() {
		return menuService.getMenuList();
	}
}
```

**MenuService 클래스**

```java
public class MenuService {
	public List<Menu> getMenuList() {
		return null;
	}
}
```

위 코드는 의존성 주입이 일어나는 예제이다.

MenuService의 기능을 사용하기 위해 MenuController 생성자로 MenuService의 객체를 전달 받고 있다.

이처럼 어떤 클래스의 객체를 전달 받는 것을 의존성 주입이라고 한다.

생성자의 파라미터로 객체를 전달하는 것을 외부에서 객체를 주입한다고 표현할 수 있다.

여기서 말하는 외부는 Client 클래스가 MenuController의 생성자 파라미터로 menuService를 전달하고 있기 때문에 객체를 주입해주는 외부가 된다.

## DI(의존성 주입)가 사용되는 이유

객체지향 언어인 Java에서는 생성자를 통해 객체를 전달하는 일이 자주 발생한다.

DI는 클래스 내부에서 외부 클래스의 객체를 생성하기 위한 **new 키워드를 쓸지 말지 결정**하는 것이기도 하다.

일반적으로 Java에서는 new 키워드를 통해 객체를 생성하는데, Reflection이라는 기법을 이용하여 Runtime시에 객체를 동적으로 생성할 수 있는 방법이 있기 때문이다.

또한, 애플리케이션 코드 내부에서 new 키워드를 사용할 경우 객체지향 설계의 관점에서 중요한 문제가 발생할 수 있다.

예를 들어, 새로운 요구 사항이 들어와 MenuService를 MenuServiceStub으로 수정해야 하는 상황이라 가정한다.

스텁(Stub)은 메서드가 호출되면 미리 준비된 데이터를 응답하는 것이다. 즉, 고정된 데이터를 호출하는 것이기 때문에 여러 번 호출하더라도 동일한 데이터를 리턴한다. (멱등성을 가진다.)

**Client 클래스**

```java
public class Client {
	public static void main(String[] args) {
		MenuServiceStub menuService = new MenuServiceStub();
		MenuController controller = new MenuController(menuService);
		List<Menu> menuList = controller.getMenus();
	}
}
```

**MenuController 클래스**

```java
public class MenuController {
	private MenuServiceStub = menuService;
	
	public MenuController(MenuServiceStub menuService) { 
		this.menuService = menuService;
	}

	public List<Menu> getMenus() {
		return menuService.getMenuList();
	}
}
```

**MenuService 클래스**

```java
public class MenuServiceStub {
	public List<Menu> getMenuList() {
		return List.of(
				new Menu(1, "아메리카노", 2000),
				new Menu(2, "카페라떼", 3000),
		);
	}
}
```

위 코드는 메뉴 목록 조회를 API로 Stub을 제공하기 위해 MenuServiceStub 클래스로 변경하고, MenuServiceStub 클래스의 getMenuList() 메서드를 통해 stub을 작성한 위 예시에서 수정된 코드이다.

이처럼 특정 요구사항에 의해 의존 관계에서 클래스를 변경해야 하는 상황이 발생한다면,

MenuService 클래스에서 MenuServiceStub 클래스로 수정하는 경우 MenuService 클래스가 사용된 모든 곳에서 수정을 해야한다.

이는 매번 수정하는 작업이 일어나면 효율적이지 않으며 실수로 인해 버그가 발생할 수 있다.

따라서 new 연산자를 사용하여 의존 객체를 생성하는 것은 강한 결합(Tight Coupling)이라 한다.

결론적으로 의존성 주입(DI)을 하더라도 클래스 간의 강한 결합은 피하는 것이 좋다.

즉, 느슨한 결합(Loose Coupling)이 필요하다.

## 느슨한 결합(Loose Coupling)

Java에서 클래스들 간의 관계를 느슨하게 만드는 방법은 인터페이스(Interface)를 사용하는 것이다.

![DI2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0adea505-f53f-4ece-812c-ce36d410e44a/DI2.png)

위 그림은 인터페이스를 사용하여 클래스 간의 느슨한 결합을 나타내는 다이어그램이다.

MenuService 클래스를 직접 생성하는 것이 아닌, 인터페이스를 생성하여

실제 서비스는 MenuServiceImpl 클래스와 MenuServiceStub 클래스에서 구현하는 것이다.

MenuController는 클래스가 아닌 MenuService 인터페이스에 의존하게 되지만, 실제 구현체인 MenuServiceImpl 클래스와 MenuServiceStub 클래스는 알지 못하게 된다.

이처럼 특정 클래스가 인터페이스와 같이 일반화된 구성 요소에 의존하고 있을 때, 클래스들 간에 느슨한 결합(Loose Coupling)이 이루어졌다고 할 수 있다.

이를 코드로 표현하면 다음과 같다.

**Client 클래스**

```java
public class Client {
	public static void main(String[] args) {
		MenuService menuService = new MenuService();
		MenuController controller = new MenuController(menuService);
		List<Menu> menuList = controller.getMenus();
	}
}
```

**MenuController 클래스**

```java
public class MenuController {
	private MenuService = menuService;
	
	// 생성자의 파라미터를 MenuService 인터페이스로 입력받음
	public MenuController(MenuService menuService) { 
		this.menuService = menuService;
	}

	public List<Menu> getMenus() {
		return menuService.getMenuList();
	}
}
```

**MenuService 인터페이스**

```java
public interface MenuService {
	List<Menu> getMenuList();
}
```

**MenuServiceStub 클래스**

```java
public class MenuServiceStub implements MenuService {
	@Override
	public List<Menu> getMenuList() {
		return List.of(
				new Menu(1, "아메리카노", 2000),
				new Menu(2, "카페라떼", 3000),
		);
	}
}
```

이와 같이 작성하여 MenuController는 Stub 클래스를 입력 받을 수 있으면서 아무런 변경이 발생하지 않도록 할 수 있다.

또한, MenuService는 인터페이스이기 때문에 MenuService의 구현 클래스라면 어떤 클래스도 모두 주입받을 수 있게 된다.

이처럼 인터페이스 타입의 변수에 해당 인터페이스의 구현 객체를 할당할 수 있다면 이를 업캐스팅(Upcasting)이라 한다.

결론적으로 위 코드는 DI(의존성 주입)를 통해 MenuController와 MenuService는 느슨한 결합 관계를 유지할 수 있게 되었다.

## new 연산자 제거

하지만, 클래스들 간의 관계를 느슨하게 만들기 위해서는 new 연산를 사용하지 않아야 한다.

이는 Spring이 대신하도록 설정할 수 있다.

**Client 클래스**

```java
public class Client {
	public static void main(String[] args) {
		GenericApplicationContext context = new AnnotationConfigApplicationContext(Config.class);
		MenuController controller = context.getBean(MenuController.class);
		List<Menu> menuList = controller.getMenus();
	}
}
```

**MenuController 클래스**

```java
public class MenuController {
	private MenuService = menuService;
	
	@Autowired
	public MenuController(MenuService menuService) { 
		this.menuService = menuService;
	}

	public List<Menu> getMenus() {
		return menuService.getMenuList();
	}
}
```

**Config**

```java
@Configuration
@ComponentScan(basePackageClasses = Client.class)
public class Config {
	@Bean
	public MenuService getMenuService() {
		return new MenuServiceStub();
	}

	@Bean
	public MenuController getMenuController(MenuService menuService) {
		return new MenuController(menuService);
	}
}
```

다음과 같이 Spring에서 지원하는 API를 통해 controller 인스턴스를 생성할 때 new 연산자를 사용하지 않을 수 있다.

하지만 POJO 프로그래밍을 위한 규칙을 위반하는 것으로 좋은 개발 방식은 아니므로 자세히 알아둘 필요는 없다.

단지, 의존성 주입(DI)의 예시를 보여주기 위한 코드일 뿐이다.

## 정리

1. IoC는 애플리케이션의 흐름이 사용자에게 있는 것이 아닌 프레임워크나 서블릿 컨테이너 등 외부에 있는 것으로 흐름의 제어권이 뒤바낀 것이다.
2. DI는 IoC 개념을 구체화 시킨 것으로 객체 간의 관계를 느슨하게 해준다.
3. 클래스 내부에서 다른 클래스의 객체를 생성하게 되면 객체 간의 관계가 성립된다.
4. new 연산자를 사용하여 객체를 직접 생성하지 않고 생성자를 외부에서 다른 클래스의 객체를 전달 받고 있다면 의존성 주입이 이루어지고 있는 것이다.
5. new 연산자를 사용하여 객체를 생성하는 것은 클래스 간의 강한 결합이다.
6. 특정 클래스가 인터페이스 같이 일반화된 구성 요소에 의존하고 있을 때, 클래스 간의 느슨한 결합이 되어 있는 것이다.
7. 객체들 간의 느슨한 결합은 요구 사항의 변경에 유연하게 대처할 수 있게 한다.