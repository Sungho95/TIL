## 애스펙트(Aspect)

- 여러 객체에 공통으로 적용되는 기능 (공통 기능)
- 어드바이스(Advice) + 포인트컷(PointCut)을 모듈화하여 애플리케이션에 포함되는 횡단 기능(Cross-cutting Concerns**)**
- 여러 개의 어드바이스와 포인트컷이 함께 존재

## 조인 포인트(join point)

![AOP 용어.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f9d012b-7aaf-41a2-a370-0dfe4c5bab46/AOP_%EC%9A%A9%EC%96%B4.png)

위 이미지의 S는 메서드 실행 전의 포인트이고, E는 메서드 실행 후의 포인트이다. S와 같은 포인트를 어드바이스가 적용될 조인포인트라고 한다.

- 클래스 초기화, 객체 인스턴스화, 메서드 호출, 필드 접근, 예외 발생과 같은 애플리케이션 실행 흐름에서의 특정 포인트를 의미한다.
- 애플리케이션에 새로운 동작을 추가하기 위해 조인포인트에 관심 코드(Aspect code)를 추가할 수 있다.
- 횡단 관심은 조인포인트 전/후에 AOP에 의해 자동으로 추가된다.
- 조인 포인트는 추상적인 개념으로 AOP를 적용할 수 있는 모든 지점이라 해석할 수 있다.
- **스프링 AOP는 프록시 방식을 사용**하여 조인포인트가 항상 **메서드의 실행 지점으로 제한**된다.
- 어드바이스 적용이 필요한 곳은 애플리케이션 내에 메서드를 갖는다.

## 어드바이스(Advice)

- 조인포인트에서 수행되는 코드를 의미
- Aspect를 언제 핵심 코드에 적용할 지 정의
- 시스템 전체 Aspect에 API 호출 제공

## 포인트컷(PointCut)

- 조인 포인트 중에서 어드바이스가 적용될 위치를 선별하는 기능
- AspectJ 표현식을 사용하여 지정
- 프록시를 사용하는 스프링 AOP는 메서드 실행 지점만 포인트컷으로 선별 가능하다.

## 위빙(Weaving)

- 포인트컷으로 결정한 타겟의 조인 포인트에 어드바이스를 적용하는 것으로 Advice를 핵심 코드에 적용하는 것이다.
- 핵심 기능 코드에 영향을 주지 않고 부가 기능을 추가할 수 있다.
- AOP 적용을 위해 Aspect 객체에 연결한 상태를 뜻한다.
    - 컴파일 타임(AspectJ compooiler)
    - 로드 타임
    - 런타임
    - 스프링 AOP는 런타임, 프록시 방식

## AOP 프록시(Proxy)

- AOP 기능을 구현하기 위해 만든 프록시 객체
- 스프링에서 AOP 프록시는 JDK 동적 프록시 또는 CGLIB 프록시를 뜻함

## 타겟(Target)

- 핵심 기능을 담고 있는 모듈로 타겟은 부가기능을 부여할 대상이 된다.
- Advice를 받는 객체이고 포인트컷으로 결정된다.

## 어드바이저(Advisor)

- 하나의 어드바이스와 하나의 포인트컷으로 구성된다.
- 스프링 AOP에서만 사용되는 특별한 용어이다.

# 타입별 Advice

## 어드바이스(Advice)

- Aspect를 언제 핵심 코드에 적용할지를 정의
- 특정 조인 포인트에서 애스펙트에 의해 취해지는 조치

## Advice 순서

기본적으로 어드바이스는 순서를 보장하지 않는다.

순서를 지정하기 위해서는 @Aspect 적용 단위로 org.springframework.core.annotation.@Order 어노테이션을 적용해야 한다.

- 어드바이스 단위가 아닌 클래스 단위로 적용할 수 있다.
- 하나의 애스펙트에 여러 어드바이스가 존재하면 순서를 보장 받을 수 없다.

애스펙트를 별도의 클래스로 분리해야 한다.

## Advice 종류

**Before**

- 조인 포인트 실행 이전에 실행한다.
- 타겟 메서드가 실행되기 전에 처리해야할 필요가 있는 부가 기능을 호출하기 전에 공통 기능을 실행한다.
- Before Advice 구현한 메서드는 일반적으로 리턴타입이 void이다.
    - 리턴 값을 가지고 있더라도 실제 Advice 적용 과정에 영향을 끼치지 않는다.
- 주의할 점은 메서드에서 예외를 발생시킬 경우 대상 객체의 메서드가 호출되지 않게 된다는 점이다.

```java
@Before("hello.aop.order.aop.Pointcuts.orderAndService()")
public void doBefore(JoinPoint joinPoint) {
    log.info("[before] {}", joinPoint.getSignature());
}
```

**AfterReturning**

- 조인 포인트가 정상 완료된 후 실행한다.
- 메서드가 예외 없이 실행된 이후에 공통 기능을 실행한다.

```java
@AfterReturning(value = "hello.aop.order.aop.Pointcuts.orderAndService()", returning = "result")
public void doReturn(JoinPoint joinPoint, Object result) {
    log.info("[return] {} return={}", joinPoint.getSignature(), result);
}
```

**AfterThrowing**

- 메서드가 예외를 던지는 경우에 실행한다.
- 메서드를 실행하는 도중에 예외가 발생하는 경우 공통 기능을 실행한다.

```java
@AfterThrowing(value = "hello.aop.order.aop.Pointcuts.orderAndService()", throwing = "ex")
public void doThrowing(JoinPoint joinPoint, Exception ex) {
    log.info("[ex] {} message={}", joinPoint.getSignature(), ex.getMessage());
}
```

**After (finally)**

- 조인 포인트의 동작(정상 종료 또는 예외 발생)과는 상관 없이 실행한다.
- 메서드 실행 후 공통 기능을 실행한다.
- 일반적으로 리소스를 해제하는데 사용한다.

**Around**

- 메서드 호출 전후에 수행하며 가장 강력한 어드바이스이다.
    - 조인 포인트 실행 여부 선택, 반환 값 변환, 예외 변한 등이 가능하다.
    - joinPoint.proceed() : 조인 포인트 실행 여부 선택
    - joinPoint.proceed(args[]) : 전달 값 변환
    - 반환 값 변환
    - 예외 변환
- 메서드 실행 전과 후, 예외 발생 시점에 공통 기능을 실행한다.
- 어드바이스의 첫 번째 파라미터는 ProceedingJoinPoint를 사용해야 한다.
- proceed()를 통해 대상을 실행한다.
- proceed()는 여러번 실행할 수 있다.

## Around

Around는 가장 강력한 어드바이스로 대부분의 기능을 제공한다. 하지만, 타겟 등 고려해야할 사항이 있을 때 정상적으로 작동이 되지 않는 경우가 있다.

- @Before, @After와 같은 어드바이스는 기능은 적지만 원하는대로 작동되고 코드도 단순하다.
- 좋은 설계는 @Around만 사용해서 모두 해결하는 것 보다는 제약을 가지더라도 실수를 방지하는 것이 좋다.
- 제약을 두면 문제 자체가 발생하지 않게 하며, 역할이 명확해 진다.