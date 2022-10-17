## Spring AOP

Spring AOP는 스프링 IoC를 보완하여 매우 강력한 미들웨어 솔루션을 제공한다.

- @AspectJ 어노테이션
- 스키마 기반 접근

## @AspectJ

@AspectJ는 어노테이션이 있는 일반 Java 클래스로 관점을 선언하는 방식을 말한다.

- @AspectJ 스타일은 AspectJ 5 릴리스의 일부로 AspectJ 프로젝트에 의해 도입되었다.
- 스프링은 pointcut 구문 분석 및 일치를 위해 AspectJ가 제공하는 라이브러리를 사용하여 AspectJ 5와 동일한 어노테이션을 해석한다.
- AOP 런타임은 여전히 순수한 스프링 AOP이며, AspectJ 컴파일러나 위버에 의존하지 않는다.

## @AspectJ 활성화

Spring에서 @AspectJ aspect를 사용하기 위해서는 Spring 설정에서 @AspectJ aspect에 기반한 Spring AOP 설정과 aspect에 의해 조인되는 자동 프록시 빈에 대한 Spring 지원을 활성화해야 한다.

@AspectJ 지원은 XML 또는 Java 스타일 설정으로 사용이 가능하다.

**Java 설정**

@Configuration으로 @AspectJ 지원을 활성화하려면 @EnableAspectJAutoProxy 어노테이션을 추가한다.

```java
@Configuration
@EnableAspectJAutoProxy
public class AppConfig {

}
```

**XML 설정**

XML 기반 구성으로 @AspectJ 지원을 활성화하려면 aop:aspectj-autoproxy 요소를 사용한다.

```xml
<aop:aspectj-autoproxy/>
```

## Aspect 선언

@AspectJ 지원이 활성화되면 @AspectJ 관점(@Aspect 어노테이션)이 있는 클래스로 애플리케이션 컨텍스트에 정의된 모든 빈이 Spring에서 자동으로 감지되고 Spring AOP를 구성하는 데 사용된다.

**XML**

```xml
<bean id="myAspect" class="org.xyz.NotVeryUsefulAspect">
    <!-- configure properties of the aspect here -->
</bean>
```

**Java**

```java
import org.aspectj.lang.annotation.Aspect;

@Aspect
public class NotVeryUsefulAspect {

}
```

## 포인트컷 선언

포인트컷은 관심 조인 포인트를 결정하므로 어드바이스가 실행되는 시기를 제어할 수 있다.

Spring AOP는 Spring Bean에 대한 메서드 실행 조인 포인트만 지원하므로 Pointcut은 Spring Bean의 메서드 실행과 일치하는 것으로 생각할 수 있다.

Pointcut 선언은 이름과 매개변수를 포함하는 서명과 우리가 관심 있는 메서드 실행을 정확히 결정하는 Pointcut 표현식의 두 부분으로 구성된다.

pointcut 표현식은 @Pointcut 어노테이션을 사용하여 표시된다.

## 어드바이스 선언

어드바이스는 포인트컷 표현식과 연관되며 포인트컷과 일치하는 메서드 실행 전후에 실행된다.

pointcut 표현식은 명명된 pointcut에 대한 단순 참조이거나 제자리에 선언된 pointcut 표현식일 수 있다.