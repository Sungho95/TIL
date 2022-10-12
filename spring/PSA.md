![PSA.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b05eb76e-ae94-4769-b20c-95132450148a/PSA.png)

## PSA(Portable Service Abstraction)란?

PSA란 환경의 변화와 관계없이 일관된 방식의 기술로의 접근 환경을 제공하는 추상화 구조를 말한다.

특정 클래스가 추상화 된 상위 클래스를 일관되게 바라보며 하위 클래스의 기능을 사용하는 것을 PSA의 기본 개념이다.

따라서 PSA가 적용된 코드는 개발자의 기존에 작성된 코드를 수정하지 않으면서 확장할 수 있으며, 어느 특정 기술에 특화되어 있지 않는 코드이다.

Spring에서 동작할 수 있는 라이브러리들은 POJO 원칙을 지키기 위해 PSA 형태의 추상화가 되어있으며, Spring Web MVC, Spring Transaction, Spring Cache, Sprind Data, 메일 서비스 등의 다양한 PSA를 제공하고 있다.

## 서비스에 적용하는 PSA 기법

서비스 추상화(Service Abstraction)는 추상화의 개념을 애플리케이션에서 사용하는 서비스에 적용하는 기법이다.

![PSA2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d116e2d7-060e-4ffb-a0fb-348590e8e598/PSA2.png)

위 그림은 Java 콘솔 애플리케이션에서 클라이언트가 데이터베이스에 연결하기 위해 JdbcConnector를 사용하기 위한 서비스 추상화의 다이어그램이다.

즉, JdbcConnector 인터페이스가 애플리케이션에서 이용하는 하나의 서비스가 되는 것이다.

위 그림에서의 DbClient 클래스는 OracleJdbcConnector, MariaDBJdbcConnector, SQLiteJdbcConnector와 같은 구현체에 직접적으로 연결해서 얻는 것이 아닌

JdbcConnector 인터페이스를 통해 간접적으로 연결되어 Connection 객체를 얻을 수 있게 된다.

또한, DbClient 클래스에서 JdbcConnector 구현체를 사용하더라도 Connection을 얻는 방식은 getConnection() 메서드로 다른 구현체와 동일하다.

**즉, 일관된 방식으로 해당 서비스의 기능을 사용할 수 있는 것이다.**

이처럼 애플리케이션에서 특정 서비스를 이용할 때, 서비스의 기능을 접근하는 방식 자체를 일관되게 유지하면서 기술 자체를 유연하게 사용할 수 있도록 하는 것을 PSA(일관된 서비스 추상화)라고 한다.

**코드 예제**

**DbClient.java**

```java
public class DbClient {
	public static void main(String[] args) {
		JdbcConnector connector = new SQLiteJdbcConnector();

		DataProcessor processor = new DataProcessor(connector);
		processor.insert();
	}
}
```

**DataProcessor.java**

```java
public class DataProcessor {
	private Connection connection;

	public DataProcessor(JdbcConnector connector) {
		this.connection = connector.getConnection();
	}

	public void insert() {
		System.out.println("inserted data");
	}
}
```

**JdbcConnector.java**

```java
public interface JdbcConnector {
	Connection getConnection();
}
```

**MariaDBJdbcConnector.java**

```java
public class MariaDBJdbcConnector implements JdbcConnector {
	@Override
	public Connection getConnection() {
		return null;
	}
}
```

**OracleJdbcConnector.java**

```java
public class OracleJdbcConnector implements JdbcConnector {
  @Override
  public Connection getConnection() {
    return null;
  }
}
```

**SQLiteJdbcConnector.java**

```java
public class SQLiteJdbcConnector implements JdbcConnector {
  @Override
  public Connection getConnection() {
    return null;
  }
}
```

위 6개의 Java 코드는 다이어그램 이미지를 기반으로 JdbcConnector 서비스를 사용하는 예제 코드이다.

DbClient 클래스는 SQLiteJdbcConnector 구현체의 객체를 생성하여 JdbcConnector 인터페이스 타입의 변수에 할당한다. (업캐스팅)

이후 데이터를 저장하는 기능을 하는 DataProcessor 클래스의 생성자로 JdbcConnector 객체를 전달하고 있다. (DI : 의존성 주입)

만약, 다른 애플리케이션에서 SQLite 데이터베이스를 사용하는 것이 아닌 Oracle이나 MariaDB를 사용해야 한다면, JdbcConnector 서비스 모듈을 그대로 사용하여

new SQLiteJdbcConnector()를 new OracleJdbcConnector() 또는 new MariaDBJdbcConnector()으로 바꿔서 사용하면 된다.

## PSA가 필요한 이유

![PSA3.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c9781dba-6aeb-4557-ae40-c098a55c0fc2/PSA3.png)

PSA는 어떤 서비스를 이용하기 위한 접근 방식을 일관된 방식으로 유지하여 애플리케이션에서 사용하는 기술이 변경되더라도 최소한의 변경만으로 변경된 요구 사항을 반영하기 위해 사용한다.

즉, PSA를 통해서 애플리케이션의 요구 사항 변경에 유연하게 대처할 수 있다.

Spring은 상황에 따라 기술이 바뀌더라도 변경된 기술에 일관된 방식으로 접근할 수 있는 PSA를 지원하고 있다. Spring Web MVC, Spring Transaction, Spring Cache, Spring Data, 메일 서비스 등이 있다.