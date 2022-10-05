## SQL이란?

SQL(Structured Query Language)을 직역하면 구조화된 Query언어이다. SQL은 관계형 데이터베이스(RDBMS)에서 데이터를 관리하고 처리하기 위해 설계된 프로그래밍 언어이다.

여기서 Query는 질의문을 뜻한다. 저장되어 있는 정보를 필터링 하기 위한 질문으로 검색창에 적는 검색어도 Query의 일종이다.

즉, SQL은 데이터베이스에 query를 보내 원하는 데이터만을 뽑아올 수 있도록 하는 언어이다.

SQL을 사용하기 위해서는 데이터의 구조가 고정되어 있어야 한다.

## 데이터베이스의 필요성

전통적인 데이터를 처리하는 방법으로 파일 입출력(File I/O)을 통해 엑셀과 같은 스프레드 시트에 데이터를 저장하거나, 인메모리(In-memory) 형태로 데이터를 임시 저장하여 사용하는 방법이 있다. 이후 데이터를 관리하고 처리하는 것에 특화된 데이터베이스로 데이터를 처리하는 방법이 등장했다.

**In-memory**

JavaScript에서 데이터를 다룰 때에는 프로그램이 실행될 때에만 존재하는 데이터가 있다.

JavaScript에서 변수를 만들어 저장하여 사용할 경우, 프로그램이 종료될 때 해당 데이터는 사라진다.

즉, 변수 등에 저장한 데이터는 프로그램의 실행에 의존한다. 이러한 방식을 In-memory 방식이라 한다.

이는 예기치 못한 상황으로부터 데이터를 보호할 수 없고, 프로그램이 종료된 상태라면 데이터를 원하는 시간에 받아올 수 없으며, 데이터의 수명이 프로그램의 수명에 의존하게 된다.

**File I/O**

파일에 데이터를 저장하여 읽는 방식으로 작동하는 형태가 File I/O이다. 엑셀 시트나 CSV 같은 파일의 형태는 In-Memory에 비해 데이터를 저장하는 방식으로 적절하다. 하지만, File I/O 방식의 한계는 뚜렷하다.

- 데이터가 필요할 때마다 전체 파일을 매번 읽어야 한다. 파일의 크기가 커질 수록 느려지고 비효율적이다.
- 파일이 손상되거나 여러 개의 파일들을 동시에 다뤄야 하는 등 예기치 못한 상황이나 복잡한 데이터를 다룰 때 작업이 어려워 진다.

**Database**

데이터베이스에서는 하나의 csv 파일이나 엑셀 시트를 한 개의 테이블로 저장할 수 있다. 한번에 여러 개의 테이블을 가질 수 있기 때문에 SQL 언어를 활용해 데이터를 불러오기 쉽고, 대용량 데이터를 처리하기 용이하다.

하지만 SQL을 사용하지 않는 데이터베이스도 존재한다. 이는 데이터의 구조가 고정되어 있지 않은 데이터베이스로 NoSQL이라 한다.

관계형 데이터베이스와는 달리 테이블을 사용하지 않고 데이터를 다른 형태로 저장한다.

NoSQL의 대표적인 예시는 MongDB와 같은 문서 지향 데이터베이스가 있다.

## SQL 문법

SQL 문법은 데이터 정의어(DDL), 데이터 조작어(DML), 데이터 제어어(DCL) 세 가지로 구분된다.

**데이터 정의어(DDL : Data Definition Language)**

DDL은 각 릴레이션을 정의하기 위해 사용하는 언어이다.

CREATE : 테이블 생성

```sql
CREATE TABLE 고객 (
		아이디 VARCHAR(20) NOT NULL,
		이름 VARCHAR(10) NOT NULL,
		나이 INT,
		직업 VARCHAR(20)
);
```

DROP : 테이블 삭제

```sql
DROP TABLE 고객 RESTRICT;
```

ALTER : 테이블 수정

추가

```sql
ALTER TABLE 고객 ADD 주소 VARCHAR(30) NOT NULL;
```

삭제

```sql
ALTER TABLE 고객 DROP 주소 CASCADE;
```

TRUNCATE : 테이블에 있는 모든 데이터 삭제

```sql
TRUNCATE TABLE 고객;
```

**데이터 조작어(DML : Data Manipulation Language)**

DML은 데이터를 추가, 수정, 삭제 등을 하기 위한 언어이다.

SELECT : 테이블에 저장된 데이터 추출

```sql
SELECT [ ALL | DISTINCT ] 속성_리스트
FROM 테이블
[ WHERE 조건 ]
[ GROUP BY 속성 리스트 [HAVING 조건] ];
[ ORDER BY 속성 리스트 [ASC | DESC] ];
```

FROM : 결과를 도출해낼 데이터베이스의 테이블을 명시한다.

WHERE : 조건에 해당한 데이터를 선택하기 위해 사용한다. (데이터의 필터링)

GROUP BY : 그룹별로 검색하기 위해 사용한다.

ORDER BY : 데이터 결과를 어떤 기준으로 정렬할 지 결정한다.

DISTINCT : 중복 값을 허용하지 않는다.

SELECT 예시

```sql
SELECT 아이디, 이름
FROM 고객;
```

```sql
SELECT *
FROM 고객
LIMIT 10;
```

애스터리스크(*) : 데이터베이스에서 애스터리스크(*)는 와일드카드(wildcard)로 전부를 의미한다.

INSERT : 테이블에 데이터 추가

```sql
INSERT
INTO 고객(아이디, 이름, 나이, 직업)
VALUES ('hello', '홍길동', '25', '회사원');
```

UPDATE : 테이블에 저장된 데이터 수정

```sql
UPDATE 고객
SET 직업 = '프로그래머'
WHERE 아이디 = 'hello'; 
```

DELETE : 테이블에 저장된 데이터 삭제

```sql
DELETE
FROM 고객
WHERE 아이디 = 'hello';
```

**데이터 제어어(DCL : Data Control Language)**

DCL은 릴레이션 또는 데이터를 관리하고, 접근 권한을 제어하는 언어이다.

GRANT : 권한 생성

```sql
GRANT 권한 ON 객체 TO 사용자;
```

검색 권한 부여

```sql
GRANT SELECT ON 고객 TO 홍길동;
```

REVOKE : 권한 삭제

```sql
REVOKE 권한 ON 객체 FROM 사용자 CASCADE | RESTRICT;
```

검색 권한 삭제

```sql
REVOKE SELECT ON 고객 FROM 홍길동 CASCADE;
```

CASCADE : 해당 사용자(홍길동)가 다른 사용자에게 부여한 권한도 함께 삭제

RESTRICT : 해당 사용자(홍길동)가 다른 사용자에게 권한을 부여한 적이 없는 경우에만 권한 삭제