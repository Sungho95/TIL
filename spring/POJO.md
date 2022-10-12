## POJO(Plain Old Java Object)

![스프링 프레임워크.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4d51a219-bec2-456a-ae87-a0a5ab16b51e/%EC%8A%A4%ED%94%84%EB%A7%81_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC.png)

위 이미지는 Spring 삼각형이라는 유명한 이미지로 Spring의 핵심 개념들을 모두 표현하고 있다.

POJO는 IoC/DI, AOP, PSA를 통해서 달성할 수 있다는 것을 의미한다.

POJO란 Plain Old Java Object의 약자로, 이를 직역하면 순수한 오래된 자바 객체이다.

즉, Java로 생성하는 순수한 객체를 뜻한다.

## POJO 프로그래밍

POJO 프로그래밍은 POJO를 이용하여 프로그래밍 코드를 작성하는 것이다.

그러나 순수 자바 객체만을 사용한다고 해서 POJO 프로그래밍이라고 볼 수는 없다.

POJO 프로그래밍으로 작성한 코드가 되기 위해서는 기본적인 규칙들을 지켜야 한다.

**1. Java나 Java의 스펙에 정의된 것 이외에는 다른 기술이나 규약에 얽매이지 않아야 한다.**

다음 코드는 getter와 setter만 가지고 있는 코드의 에제이다.

```java
public class User {
	private String userName;
	private String id;
	private String password;

	public String getUserName() {
		return userName;
	}

	public void setUserName(String userName) {
		this.userName = userName;
	}

	public String getId() {
		return id;
	}

	public void setId(String id) {
		this.id = id;
	}

	public String getPassword() {
		return password;
	}

	public void setPassword(String password) {
		this.password = password;
	}
}
```

위 코드는 자바에서 제공하는 기능만 사용하기 때문에 해당 클래스는 Java 언어 이외의 특정한 기술에 종속되어 있지 않은 순수한 객체이기 때문에 POJO라고 부를 수 있다.

다음은 특정 기술에 종속적인 예제이다.

```java
public class MessageForm extends ActionForm {
	String message;

	public String getMessage() {
		return message;
	}

	public void setMessage(String message) {
		this.message = message;
	}
}

public class MessageAction extends Action {

	public ActionForward execute(ActionMapping mapping, ActionForm form,
		HttpServletRequest request, HttpServletResponse response)
        throws Exception {
		
		MessageForm messageForm = (MessageForm) form;
		messageForm .setMessage("Hello World");
		
		return mapping.findForward("success");
	}
	
}
```

ActionForm 클래스는 과거에 Struts라는 웹 프레임워크에서 지원하는 클래스이다.

MessageForm 클래스는 Struts라는 기술을 사용하기 위해 ActionForm 클래스를 상속받고 있다.

또한, MessageAction 클래스에서 역시 Struts 기술의 Action 클래스를 상속받고 있다.

이러한 방식으로 기술을 상속 받아 코드를 작성하게 되면, 애플리케이션의 요구사항이 변경되어 다른 기술로 변경해야할 때 Struts의 클래스를 명시적으로 사용했던 부분들을 모두 제거하여 수정해야 한다.

또한, Java는 다중 상속을 지원하지 않기 떄문에 extends 키워드를 통해 상속을 받게 되면 상위 클래스를 상속받아 하위 클래스를 확장하는 객체지향 설계 기법을 적용하기 어려워진다.

**2. 특정 환경에 종속적이지 않아야 한다.**

서블릿(Servlet) 기반의 웹 애플리케이션을 실행 시키는 서블릿 컨테이너(Servlet Contatiner)인 아파치 톰캣(Apache Tomcat)을 예로 들어

순수 Java로 작성한 애플리케이션 코드 내에서Tomcat이 지원하는 API를 직접 가져다가 사용한다고 가정한다.



이후 시스템의 요구 사항이 변경되어 톰캣에서 Zetty라는 다른 서블릿 컨테이너를 사용하게 된다면,

애플리케이션 코드에서 사용하고 있는 Tomcat API 코드들을 모두 제거하고 Zetty로 수정해야 한다.

최악의 경우 애플리케이션을 전부 수정해야 하는 상황에 직면할 수도 있다.

따라서, Java 이외의 다른 기술에 얽매이지 않으며, 특정 환경에 종속적이지 다른 않아야 POJO 프로그래밍이라고 할 수 있다.

## POJO 프로그래밍이 필요한 이유

1. 특정 환경이나 기술에 종속적이지 않으면 재사용이 가능하고, 확장 가능한 유연한 코드를 작성할 수 있다.
2. 저수준 레벨의 기술과 환경에 종속적인 코드를 제거하여 코드를 간결해지며 디버깅하기에도 상대적으로 쉬워진다.
3. 특정 기술이나 환경에 종속적이지 않기 때문에 테스트가 단순해진다.
4. 객체지향적인 설계를 제한없이 적용할 수 있다. (가장 중요한 이유)

## POJO와 Spring의 관계

Spring은 POJO 프로그래밍을 지향하는 프레임워크이다.

최대한 다른 환경이나 기술에 종속적이지 않도록 하기 위한 POJO 프로그래밍 코드를 작성하기 위해 Spring 프레임워크에서는 IoC/DI, AOP, PSA를 지원하고 있다.