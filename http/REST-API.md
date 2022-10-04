# REST API란 무엇인가?

## Intro

웹 애플리케이션에서는 HTTP 메서드를 이용해 서버와 통신한다.

GET을 통해 웹 페이지나 데이터를 요청하고,

POST로 새로운 글이나 데이터를 전송하며,
DELETE로 저장된 글이나 데이터를 삭제할 수 있다.

이처럼 클라이언트와 서버가 HTTP 통신을 할때는 어떤 요청을 보내고 받느냐에 따라 메서드의 사용이 달라진다.

HTTP 메서드의 사용은 아무런 규칙 없이 이루어지는 것이 아니다. 요청과 응답을 할 때에는 정확히 요청하고 응답 받을 수 있는 규약이 존재한다.

## REST란?

REST API에서 REST는 REpresentational State Transfer의 약자로, 로이 필딩의 논문에서 웹(http)의 장점을 최대한 활용할 수 있는 아키텍처로써 처음 소개되었다.

즉, REST는

HTTP URI를 통해 자원(Resource)를 명시하고,

HTTP 메서드를 통해 해당 자원에 대한 CRUD 연산을 적용한다.

**CRUD**

CRUD는 Create(생성), Read(읽기), Update(갱신), Delete(삭제)를 묶어서 일컫는 말이다. 사용자 인터페이스가 갖추어야 할 기능(정보의 참조, 검색, 갱신)을 가리키는 용어로도 사용된다.

## REST 아키텍처의 조건

REST는 6가지 조건을 준수하면 개별 컴포넌트를 자유롭게 구현할 수 있다.

1. 인터페이스의 일관성 : 일관적인 인터페이스로 분리되어야 한다.
2. 무상태 : 요청한 클라이언트의 콘텍스트가 서버에 저장되어서는 안된다.
3. 캐시 처리 가능 : 클라이언트는 응답을 캐싱할 수 있어야 한다.
4. 계층화 : 클라이언트는 서버에 직접 연결되었는지, 중간 서버를 통해 연결되었는지를 알 수 없기 때문에 중간 서버는 로드 밸런싱 기능이나 공유 캐시 기능을 제공함으로써 시스템 규모 확장성을 향상시킨다.
5. Code on demand (optional) : 자바 애플릿이나 자바스크립트의 제공을 통해 서버는 클라이언트가 실행시킬 수 있는 로직을 전송하여 기능을 확장시킬 수 있다.
6. 클라이언트-서버 구조 : 아키텍처를 단순화시키고 작은 단위로 분리하여 클라이언트-서버의 각 파트가 독립적으로 개선될 수 있도록 한다.

## REST의 장단점

**장점**

1. HTTP 프로토콜을 그대로 사용하여 REST API 사용을 위한 별도의 기능을 구현할 필요가 없다.
2. HTTP 프로토콜의 표준을 활용하여 추가적인 장점을 이용할 수 있다.
3. HTTP 표준 프로토콜에 다르는 모든 플랫폼에서 사용이 가능하다.
4. Hypermedia API의 기본을 지키면서 범용성을 보장한다.
5. REST API 메시지가 의도하는 바를 쉽게 파악할 수 있다.
6. 여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
7. 서버와 클라이언트의 역할을 명확하게 분리한다.

**단점**

1. 표준이 존재하지 않아 정의가 필요하다.
2. 사용할 수 있는 메서드가 4가지로 한정적이다.
3. HTTP 메서드 형태가 제한적이다.
4. 브라우저를 통해 많은 테스트를 요구한다면, URI보다 Header 정보의 값을 처리해야 하기 때문에 전문성이 요구된다.
5. 구형 브라우저(인터넷 익스플로러)에서 호환이 되지 않아 지원하지 않는 동작이 많다.

## REST API란?

REST API는 REST의 원리를 따르는 것을 기반으로 만들어진 API이다. 웹에서 사용되는 데이터나 자원(Resource)을 HTTP URI로 표현하고, HTTP 프로토콜을 통해 요청과 응답을 정의하는 방식을 말한다.

## RESTful이란?

RESTful은 REST 원리를 따르는 시스템을 의미한다. 즉, REST를 사용했다 하여도 모두가 RESTful 한 것이 아니다.

REST API의 설계 규칙을 올바르게 지켜야 해당 시스템을 RESTful하다고 말할 수 있다.

API의 모든 CRUD 기능을 POST로 처리한다거나, URI 규칙을 올바르게 지키지 않는 API는 REST API의 설계 규칙을 지키지 못한 시스템이다.

이러한 경우 REST API를 사용하였지만, RESTful 하지 못한 시스템이라고 할 수 있다.

## REST API 기본 설계 규칙

REST API를 설계할 때, 보편적인 답이 존재하지 않아 어려움을 겪을 수 있다. REST 설계의 모범 사례는 여전히 논의되고 있으며 통합하고 있다. 이는 REST API의 설계에 큰 도움이 될 것이다.

**리소스(URI)를 작성할 때 소문자를 사용한다.**

대문자는 문제를 일으키는 요소가 될 수 있기 때문에 URI를 작성할 때는 소문자로 작성한다.

RFC3986은 체계 및 호스트 구성요소를 제외하고 URI를 대소문자로 구분하여 정의한다.

Bad case : http://restapi.example.com/HelloWorld
Good case : http://restapi.example.com/helloworld

**언더바(_)대신 하이픈(-)을 사용한다.**

가독성을 위해 긴 Path를 표현하는 경우 하이픈으로 구분하는 것이 좋다.

프로그램의 글자 폰트에 따라서 언더바 문자는 부분적으로 가려지거나 숨겨질 수 있어 하이픈을 사용한다.

Bad case : http://restapi.example.com/hello_world
Good case : http://restapi.example.com/hello-world

**URI 마지막에는 슬래시(/)를 포함하지 않는다.**

후행 슬래쉬는 의미가 없고 혼란을 야기할 수 있다.

많은 웹 구성 요소와 프레임워크에서는
http://restapi.example.com/hello-world/
http://restapi.example.com/hello-world
두 URI를 동등하게 취급한다.

그러나 URI 내의 모든 문자는 리소스의 고유 ID에 포함되어 두 개의 다른 URI는 두 개의 다른 리소스에 매핑된다.

REST API는 명확한 URI를 생성해야 한다.

Bad case : http://restapi.example.com/hello-world/
Good case : http://restapi.example.com/hello-world

**계층 관계를 나타낼 때는 슬래시(/)를 사용하여 구분한다.**

슬래시(/) 문자는 URI의 경로 부분에서 자원 간의 계층적 관계를 나타내기 위해 사용한다.

Good case : http://restapi.example.com/hello-world/1

**행위를 포함하지 않는다.**

행위는 URL대신 메서드를 사용하여 전달한다.

Bad case : http://restapi.example.com/get-number

Good case : http://restapi.example.com/number

**파일 확장자는 URI에 포함시키지 않는다.**

파일 확장자는 URI에 포함하지 않고 Content-Type이라는 헤더를 통해 전달되는 대로 미디어 타입을 사용하여 body의 컨텐츠를 처리하는 방법을 결정한다.

REST API 클라이언트는 HTTP에서 제공하는 Accept 요청 헤더를 활용하도록 권장해야 한다.

Bad case : http://restapi.example.com/image.png

Good case : http://restapi.example.com/image

**컨트롤 자원을 제외하고는 명사를 사용해야 한다.**

컨트롤 자원의 경우 예외적으로 동사를 허용한다.

Bad case : http://restapi.example.com/reading

Good case : http://restapi.example.com/read