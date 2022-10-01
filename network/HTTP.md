## HTTP(HyperText Transfer Protocol)

HTTP는 HyperText Transfer Protocol의 줄임말로, 직역하면 하이퍼텍스트 전달 프로토콜이다.

하이퍼텍스트(HyperText)는 인터넷 사용자가 필요한 정보의 자유로운 검색을 가능하도록 해주는 텍스트의 전개방식이다.

HTTP는 이러한 하이퍼텍스트 방식의 정보를 교환하기 위한 하나의 규칙이다.

즉, HTML과 같은 문서를 전송하기 위해 사용되며 OSI 7계층에서 응용 계층에 있는 프로토콜이다.

HTTP는 웹 브라우저와 웹 서버의 소통을 위해 디자인 되었으며, 전통적인 클라이언트-서버 아키텍처 모델에서 클라이언트가 HTTP 메시지 양식에 맞춰 요청을 보내면, 이에 서버는 HTTP 메시지 양식에 맞춰 응답을 한다.

HTTP는 특정 상태를 유지하지 않는 무상태성(Stateless)이 특징이다.

## HTTP 메시지(HTTP messages)

HTTP 메시지는 클라이언트와 서버 사이에서 데이터가 교환되는 방식이다.

HTTP 메시지는 텍스트 정보를 구성하며 구성 파일, API, 기타 인터페이스에서 HTTP 메시지를 자동으로 완성한다.

HTTP 메시지에는 요청(Request)과 응답(Response) 두 가지 유형이 있다.

![HTTP1.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4e53e6b6-bd52-4d96-a460-f24330f90706/HTTP1.png)

HTTP 메시지의 요청과 응답은 유사한 구조를 가진다.

- Start line : 요청의 상태를 나타내며, 항상 첫 번째 줄에 위치한다.
- Status line : 응답의 상태를 나타내며, 항상 첫 번째 줄에 위치한다.
- HTTP headers : 요청을 지정하거나 메시지에 포함된 본문을 설명하는 헤더의 집합이다.
- empty line : 헤더와 본문을 구분하는 빈 줄이다.
- body : 요청과 관련된 데이터나 응답과 관련된 데이터 또는 문서를 포함한다. 요청과 응답의 유형에 따라 선택적으로 사용한다.

start line과 HTTP headers를 묶어 요청의 헤드(head),

status line과 HTTP headers를 묶어 응답의 헤드(head)라 한다.

## 요청(Requests)

HTTP Requests는 클라이언트가 서버에 보내는 메시지이다.

**Start line**

Start line에는 세 가지 요소가 있다.

1. 수행할 작업(GET, PUT, POST 등)이나 방식(HEAD, OPTIONS)을 설명하는 HTTP 메서드를 나타낸다.
2. 요청 대상(URL 또는 URI) 또는 프로토콜, 포트, 도메인의 절대 경로 등은 요청 컨텍스트에 작성되며 HTTP 메서드마다 다르게 작성된다.
3. HTTP 버전에 따라 HTTP 메서드의 구조가 달라진다. 따라서 start line에 HTTP 버전을 함께 입력된다.

**Headers**

HTTP Requests의 Headers는 기본 구조를 따른다.

헤더의 이름, 콜론, 값 형태로 입력되며 값은 헤더에 따라 다르다.

여러 종류의 헤더가 있다.

![HTTP2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8365246f-e669-402f-9836-d5acda59ff73/HTTP2.png)

일반 헤더(General headers) : 메시지 전체에 적용되는 헤더로 body를 통해 전송되는 데이터와는 관련이 없는 헤더이다.

요청 헤더(Request headers) : fetch를 통해 가져올 리소스나 클라이언트 자체에 대한 자세한 정보를 포함하는 헤더를 의미한다. User-Agent, Accept-Type, Accept-Language와 같은 헤더는 요청을 보다 구체화한다. Referer처럼 컨텍스트를 제공하거나 If-None과 같이 조건에 따라 제약을 추가할 수 있다.

표현 헤더(Representation headers) : body에 담긴 리소스의 정보(콘텐츠 길이, MIME 타입 등)를 포함하는 헤더이다.

**Body**

Body는 요청의 본문으로 HTTP 메시지 구조의 마지막에 위치한다.

모든 요청에 body가 필요한 것은 아니다.

GET, HEAD, DELETE, OPTIONS처럼 서버에 리소스를 요청하는 경우에는 본문이 필요하지 않는다.

단, POST나 PUT과 같은 일부 요청에 대해서는 데이터를 업데이트하기 위해 body를 사용한다.

body는 단일-리소스 바디와 다중-리소스 바디로 구분된다.

단일-리소스 바디(Single-resource bodies) : 헤더 두 개(Content-Type과 Content-Length)로 정의된 단일 파일로 구성된 바디이다.

다중-리소스 바디(Multiple-resource bodies) : 여러 파트로 구성된 바디에서 각 파트마다 다른 정보를 지닌다. 보통 HTML form과 관련이 있다.

## 응답(Responses)

HTTP Responses는 클라이언트의 요청을 서버가 응답하는 것이다.

**Status line**

응답의 첫 줄에는 Status line이 포함되며 다음과 같은 정보를 가지고 있다.

1. 현재 프로토콜의 버전
2. 상태 코드 : 요청의 결과를 나타낸다. (200, 302, 404 등)
3. 상태 텍스트 : 상태 코드에 대한 설명

**Headers**

응답에 들어가는 HTTP headers는 요청 헤더와 동일한 구조를 가지고 있다.

대소문자 구분 없는 문자열과 콜론, 값을 입력한다.

값은 헤더에 따라 다르며 여러 종류의 헤더가 있다.

![HTTP3.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ef2ba47c-2167-4230-8ab7-333ab12e106c/HTTP3.png)

일반 헤더(General headers) : 메시지 전체에 적용되는 헤더로, body를 통해 전송되는 데이터와는 관련이 없는 헤더이다.

응답 헤더(Reponse headers) : 위치 또는 서버 자체에 대한 정보(이름, 버전 등)와 같이 응답에 대한 부가적인 정보를 갖는 헤더이다. Vary, Accept-Ranges와 같은 상태 줄에 넣기에는 공간이 부족한 추가 정보를 제공한다.

표현 헤더(Representation headers) : body에 담긴 리소스의 정보(콘텐츠 길이, MIME 타입 등)를 포함하는 헤더이다.

**body**

응답의 바디에는 HTTP 메시지 구조의 마지막에 위치한다.

모든 응답에 body가 필요하지는 않는다.

201, 204와 같은 상태 코드를 가지는 응답에는 본문을 필요로 하지 않는다.

응답의 body는 단일-리소스 바디와 다중-리소스 바디로 구분된다.

단일-리소스 바디(Single-resource bodies) : 길이가 알려진 단일-리소스 바디는 두 개의 헤더(Content-Type, Content-Length)로 정의한다.

길이를 모르는 단일 파일로 구성된 단일-리소스 바디는 Transfer-Encoding이 chunked로 설정되어 있으며, 파일은 chunk로 나뉘어 인코딩 되어 있다.

다중-리소스 바디(Multiple-resource bodies) : 서로 다른 정보를 담고 있는 body이다.

**Stateless**

Stateless는 말 그대로 상태를 가지지 않는다는 뜻이다. HTTP로 클라이언트와 서버가 통신을 주고받는 과정에서, HTTP가 클라이언트나 서버의 상태를 확인하지 않는다.

HTTP의 특징인 무상태성을 의미한다.