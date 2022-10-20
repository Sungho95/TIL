## Spring MVC

스프링 프레임워크의 모듈 중에는 웹 계층을 담당하는 몇 가지 모듈이 있다.

웹 계층에 서블릿(Servlet) API를 기반으로 클라이언트의 요청을 처리하는 모듈이 있는데 이를 스프링 웹 MVC(spring-web-mvc)라고 한다.

우리는 이를 Spring MVC(스프링 MVC)라고도 한다. Spring MVC는 클라이언트의 요청을 편리하게 해주는 기능을 제공한다.

**서블릿(Servlet)이란?**

서블릿은 클라이언트의 요청을 처리하도록 특정 규약에 맞춰 Java 코드로 작성하는 클래스 파일이다.

아파치 톰캣(Apache Tomcat)은 이러한 서블릿들이 웹 애플리케이션으로 실행할 수 있도록 해주는 서블릿 컨테이너(Servlet Container) 중 하나이다.

Spring MVC 내부에서는 서블릿을 기반으로 웹 애플리케이션을 동작하며, 스프링 부트는 기본적으로 아파치 톰캣이 내장되어 있다.

## MVC란? (MVC: Model, View, Controller)

Spring MVC에서의 MVC는 Model, View, Controller를 의미한다.

**Model(모델)**

Spring MVC 기반의 웹 애플리케이션이 클라이언트의 요청을 전달 받으면 요청 사항을 처리하기 위한 작업을 한다.

처리한 작업의 결과 데이터를 클라이언트에게 응답을 돌려주어야 하는데, 이 때 클라이언트에게 응답으로 돌려주는 **작업의 처리 결과 데이터를 Model**이라 한다.

클라이언트의 요청 사항을 구체적으로 처리하는 영역을 서비스 계층(Service layer)라고 하며,

요청 사항을 처리하기 위해 Java 코드로 구현한 것을 비즈니스 로직(Business Logic)이라 한다.

**View(뷰)**

View는 Model을 이용하여 웹 브라우저와 같은 애플리케이션의 화면에 보여지는 리소스(Resource)를 제공하는 역할을 한다.

Spring MVC에는 다양한 View 기술이 포함되어 있다.

- HTML 페이지 출력
- PDF, Excel 등의 문서 형태로 출력
- XML, JSON 등 특정 형식의 포맷으로 변환

**Controller(컨트롤러)**

컨트롤러는 클라이언트 측의 요청을 직접적으로 전달 받는 엔드포인트(Endpoint)로써 Model과 View의 중간에서 상호작용을 해주는 역할을 한다.

클라이언트 측의 요청을 전달받아 비즈니스 로직을 거친 후, Model 데이터가 만들어지면, 이 Model 데이터를 View로 전달하는 역할을 한다.