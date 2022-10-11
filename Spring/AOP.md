![AOP.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d986fdcc-25c2-410d-afa9-19915993d2dd/AOP.png)

## AOP(Aspect Oriented Programming)란?

AOP(Aspect Oriented Programming)를 직역하면 관점 지향 프로그래밍으로 해석할 수 있다.

OOP(Object Oriented Programming)은 객체 지향 프로그래밍이다. 즉, 객체 간의 관계를 지향하는 프로그래밍 방식이다.

그렇다면 이 관점(Aspect)을 지향하는 프로그래밍은 무엇일까?

![AOP2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3f29bb3e-74b8-43e6-b108-a17830be1afc/AOP2.png)

위 그림처럼 아이를 키우는 육아 방식이나 교육 방식 등은 부모에 따라 제각각이다.

어떤 부모는 아이의 언어 발달을 위해 책을 읽어줄 것이고, 어떤 부모는 동요나 만화를 들려줄 것이다.

이처럼 아이를 키우는 방식은 다를 수 있지만, 공통되는 부분이 존재한다.

부모의 공통된 관심사는 어떤 방식으로 아이를 키우는 것과는 별개로 아프지 않고 잘 자라는 것이다.

AOP는 부모들이 가지고 있는 아이의 건강과 같은 공통 관심사와 마찬가지로 애플리케이션에 필요한 기능 중에서 공통적으로 적용되는 기능에 대한 관심과 관련이 있다.

이를 공통 관심 사항과 핵심 관심 사항으로 구분 짓는다.

## 공통 관심 사항과 핵심 관심 사항

**공통 관심 사항(Cross-cutting concern)**

애플리케이션을 개발하면서 공통적으로 사용되는 기능들이 있다. 이러한 공통 기능에 대한 관심사를 바로 공통 관심 사항이라고 한다.

**핵심 관심 사항(Core concern)**

핵심 관심 사항은 애플리케이션의 공통 기능이 아닌 비즈니스 로직에 대한 관심사로 애플리케이션의 주목적을 달성하기 위한 핵심 로직에 대한 관심 사항을 뜻한다.

**공통 관심 사항과 핵심 관심 사항의 예시**

상품을 주문하는 프로그램이 있다고 가정한다.

관리자는 고객에게 제공할 상품을 구성하기 위해 상품 등록하는 기능과

고객이 주문하고 싶은 상품을 담고 주문하는 기능은 핵심 관심 사항에 해당된다.

반면에 상품을 주문하는 프로그램에 회원만 접속할 수 있도록 제한하는 등의 보안과 상품을 결제하는 트랜잭션 등은 프로그램의 공통적으로 적용되는 기능이기 때문에 공통 관심 사항에 해당된다.

즉, AOP는 애플리케이션의 핵심 업무 로직에서 로깅이나 보안, 트랜잭션 같은 공통 기능 로직들을 분리하는 것으로 생각하면 이해하기 쉽다.

## AOP가 필요한 이유

애플리케이션의 핵심 로직과 공통 기능을 분리하는 이유는

1. 코드의 간결성 유지
2. 객체 지향 설계 원칙에 맞는 코드 구현
3. 코드의 재사용

등 과 같은 이유로 사용한다.

AOP가 적용되지 않은 코드와 AOP가 적용된 코드를 비교하여 AOP가 필요한 이유를 알 수 있다.

**AOP가 적용되지 않은 예제**

```java
import java.awt.*;
import java.lang.reflect.Member;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class NoAOP {
    private Connection connection;
    
    public void registerMember(Member member, Point point) throws SQLException {
        connection.setAutoCommit(false);
        try {
            saveMember(member);
            savePoint(point);
            
            connection.commit();
        } catch (SQLException e) {
            connection.rollback();
        }
    }
    
    private void saveMember(Member member) throws SQLException {
        PreparedStatement psMember = 
                connection.prepareStatement("INSERT  INTO  member (email, password) VALUES (?, ?)");
        psMember.setString(1, member.getEmail());
        psMember.setString(2, member.getPassword());
        psMember.executeUpdate();
    }
    
    private void savePoint(Point point) throws SQLException {
        PreparedStatement psPoint =
                connection.prepareStatement("INSERT INTO point (email, point) VALUES (?, ?)");
        psPoint.setString(1, point.getEmail());
        psPoint.setInt(2, point.getPoint());
        psPoint.executeUpdate();
    }
}
```

위 코드는 프로그램을 사용할 회원 정보를 등록하는 기능을 한다.

registerMember() 메서드 내에는 실제로 비즈니스 로직을 수행하는 코드로 saveMember()와 savePoint()이다.

또한, ‘connection.setAutoCommit(false);’와 ‘connection.commit();’, ‘connection.rollback();’은 saverMember()와 savePoint() 작업을 트랜잭션으로 묶어서 처리하기 위한 기능이다.

위 코드의 문제점은 트랜잭션 처리를 하는 코드들이 애플리케이션의 다른 기능에도 중복되어 나타날 수 있다는 것이다.

따라서 중복된 코드를 공통화해서 재사용이 가능하도록 만들 수 있다.

이러한 공통화 작업은 AOP를 통해서 할 수 있다.

**AOP가 적용된 예제**

```java
@Component
@Transactional
public class AOP {
    private Connection connection;

    public void registerMember(Member member, Point point) throws SQLException {
        saveMember(member);
        savePoint(point);
    }

    private void saveMember(Member member) throws SQLException {
        // Spring JDBC를 이용한 회원 정보 저장
    }

    private void savePoint(Point point) throws SQLException {
        // Spring JDBC를 이용한 포인트 정보 저장
    }
}
```

위 코드는 Spring의 AOP 기능을 사용하여 registerMember() 메서드에 트랜잭션을 적용한 코드이다.

해당 코드에는 비즈니스 로직을 처리하기 위한 ‘saveMember(member);’와 ‘savePoint(point)’만 작성되어 있다.

해당 코드의 트랜잭션 처리는 @Transactional 어노테이션을 통해 Spring 내부에서 해당 정보를 확인한 후, AOP 기능을 통해 트랜잭션을 적용하게 된다.

AOP는 애플리케이션에 적용되는 공통 기능(트랜잭션, 로깅, 보안, 트레이싱, 모니터링 등)을 비즈니스 로직에서 깔끔하게 분리하여 재사용 가능한 모듈로 사용할 수 있다.