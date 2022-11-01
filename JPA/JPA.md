# JPA란?(Java Persistence API)

JPA는 자바에서 사용하는 ORM(Object-Relational Mapping) 기술 표준이다.

JPA는 자바 애플리케이션과 JDBC 사이에서 동작하며, 자바 인터페이스로 정의되어 있다.

ORM은 객체와 관계형 데이터베이스를 매핑하는 기술을 의미한다.

따라서 JPA는 자바의 객체와 관계형 데이터베이스를 매핑하는 자바 표준 기술이라고 할 수 있다.

ORM을 사용하면서 객체와 테이블을 매핑하여 **패러다임 불일치 문제**를 해결할 수 있게 되었다.

## **Hibernate ORM**

JPA 표준 사양을 구현한 구현체로 Hibernate ORM, EclipseLink, DataNucleus 등이 있다. 이 중 Hibernate ORM은 JPA에서 정의한 인터페이스를 구현한 구현체이다.

JPA에서 지원하는 기능을 포함하여 자체적으로 사용할 수 있는 API 등을 지원하고 있다.

**데이터 액세스 계층**

![JPA.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2b39fbe2-1111-4714-8914-849e00ae7fe8/JPA.png)

데이터 저장, 조회 등의 작업은 JPA를 거쳐서 JPA의 구현체인 Hibernate ORM을 통해 이루어진다.

Hibernate ORM은 내부적으로 JDBC API를 이용하여 데이터베이스에 접근하는 구조이다.

## Persistence

JPA에서 P를 의미하는 단어로 영속성, 지속성이라는 뜻을 가지고 있다.

JPA는 무언가를 오래 지속되게 하는 것을 유추할 수 있다.

**영속성 컨텍스트(Persistence Context)**

ORM은 객체와 데이터베이스 테이블의 매핑을 통해 엔티티 클래스 객체 안에 포함된 정보를 테이블에 저장하는 기술이다.

JPA에서는 테이블과 매핑되는 엔티티 객체 정보를 **영속성 컨텍스트**를 통해 애플리케이션 내에서 오래 지속되도록 보관한다.

영속성 컨텍스트(Persistence Context)를 그림으로 표현하면 다음과 같이 나타낼 수 있다.

![JPA2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/84f96069-a4f6-4e55-acc2-eea984c8ccc8/JPA2.png)

영속성 컨텍스트에는 1차 캐시 영역과 쓰기 지연 SQL 저장소 영역이 있다.

JPA API 중에서 엔티티 정보를 영속성 컨텍스트에 저장하는 API를 사용하면, 영속성 컨텍스트의 1차 캐시에 엔티티 정보가 저장된다.

영속성 상태의 장점

- 1차 캐시
- 동일성(identity) 보장
- 트랜잭션을 지원하는 쓰기 지연
- 변경 감지
- 지연 로딩