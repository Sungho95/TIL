## JDBC란?

JDBC(Java Database Connectivity)는 Java 기반 애플리케이션의 데이터를 데이터베이스에 저장 및 업데이트 하거나, 데이터베이스에 저장된 데이터를 Java에서 사용할 수 있도록 하는 표준 명세이다.

JDBC는 Java 애플리케이션에서 데이터베이스에 접근하기 위해 JDBC API를 사용하여 데이터베이스에 연동할 수 있다.

뿐만 아니라, SQL 문을 자바 프로그램 내에서 실행하기 위한 여러 JDBC API도 지원하고 있다.

Spring Data JDBC, Spring Data JPA 등과 같은 기술이 등장하면서 JDBC API를 직접적으로 사용하는 일은 줄어들었다.

하지만, Spring Data JDBC, Sprind Data JPA와 같은 기술도 데이터베이스와 연동하기 위해 내부적으로 JDBC를 이용하기 때문에 JDBC의 동작 흐름에 대해 알 필요가 있다.

## JDBC의 동작 흐름

![JDBC.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b960fac1-1c00-49ed-a8e0-b787b2ca868b/JDBC.png)

JDBC는 Java 애플리케이션 내에서 JDBC API를 사용하여 데이터베이스에 접근하는 단순한 구조이다.

JDBC API를 사용하기 위해서는 JDBC 드라이버를 먼저 로딩한 후 데이터베이스와 연결하게 된다.

**JDBC 드라이버**

- 데이터베이스와의 통신을 담당하는 인터페이스
- Oracle, MS SQL, MySQL 등과 같은 데이터베이스에 알맞은 JDBC 드라이버를 구현하여 제공
- JDBC 드라이버의 구현체를 이용해서 특정 벤더의 데이터베이스에 접근할 수 있음

## JDBC API 사용 흐름

JDBC API의 구성 요소들의 동작 흐름은 다음과 같다.

![JDBC2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/777004fb-af01-4ad9-958b-bb90ad119495/JDBC2.png)

1. JDBC 드라이버 로딩 : 사용하고자 하는 JDBC 드라이버를 로딩한다. JDBC 드라이버는 DriverManager 클래스를 통해 로딩된다.
2. Connection 객체 생성 : JDBC 드라이버가 정상적으로 로딩되면 DriverManager를 통해 데이터베이스와 연결되는 세션(Session)인 Connection 객체를 생성한다.
3. Statement 객체 생성 : Statement 객체는 작성된 SQL 쿼리문을 실행하기 위한 객체로 정적 SQL 쿼리 문자열을 입력으로 가진다.
4. Query 실행 : 생성된 Statement 객체를 이용하여 입력한 SQL 쿼리를 실행한다.
5. ResultSet 객체로부터 데이터 조회 : 실행된 SQL 쿼리문에 대한 결과 데이터 셋이다.
6. ResultSet, Statement, Connection 객체들의 Close : JDBC API를 통해 사용된 객체들은 생성된 객체들을 사용한 순서의 역순으로 Close한다.

## Connection Pool

JDBC API를 사용하여 데이터베이스와 연결하기 위해 Connection 객체를 생성하는 작업은 비용이 많이 드는 작업 중 하나이다.

따라서 애플리케이션 로딩 시점에 Connection 객체를 미리 생성하고, 애플리케이션에서 데이터베이스에 연결이 필요할 경우 미리 준비된 Connection 객체를 사용하여 애플리케이션의 성능을 향상시킨다.

**Connection 객체를 미리 생성하여 보관**하고 애플리케이션이 **필요할 때 꺼내서 사용할 수 있도록 관리**해 주는 것이 **Connection Pool**이다.

![JDBC3.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7e3a2329-5ed5-4c51-b401-62a393d65877/JDBC3.png)

Spring Boot 2.0 이전 버전에서는 Apache 재단의 오픈 소스인 Apache Commons DBCP를 주로 사용하였지만, 스프링 부트 2.0 이후 HikariCP를 기본 DBCP로 채택하여 사용되고 있다.

## HikariCP란?

HikariCP는 가벼운 용량과 빠른 속도를 가지는 우수한 성능의 JDBC Connection Pool Framework이다.

스프링 부트 2.0 이후부터는 커넥션 풀을 관리하기 위해 HikariCP를 사용하고 있다.

![HikariCP-bench-2.6.0.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7d9d4d11-2536-41ad-8e37-f436459a361c/HikariCP-bench-2.6.0.png)

HikariCP는 미리 정해놓은 크기 만큼의 Connection을 Connection Pool에 담아 놓는다.

이후 요청이 들어오면 Thread가 Connection을 요청하고, Connection Pool에 있는 Connection을 연결해 준다.