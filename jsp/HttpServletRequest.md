## Intro

JSP 라이브러리에서는 HTTP 메시지를 편리하게 조회하고 사용할 수 있도록 도와주는 HttpServletRequest, HttpServletResponse 객체를 제공하고 있다.

## HttpServletRequest

HTTP 요청 메시지를 개발자가 직접 파싱해도 되지만 매우 불편할 것이다.

서블릿(Servlet)은 개발자가 HTTP 요청 메시지를 편리하게 사용할 수 있도록 HTTP 메시지를 대신 파싱한다.

이렇게 파싱된 메시지를 HttpServletRequest 객체에 담아서 제공하는 것이다.

즉, HttpServletRequest는 서블릿이 HTTP 요청 메시지를 파싱한 결과를 담은 객체이다.

HttpServletRequest를 사용하면 HTTP 요청 메시지를 편리하게 조회할 수 있게 된다.

**HTTP 요청 메시지**

![HttpServletRequest.PNG](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4a7c82a7-4f34-4679-9f9c-140b0f1ab4a7/HttpServletRequest.png)

- START LINE : HTTP 메서드, URL, 쿼리 스트링, 스키마, 프로토콜 정보가 담겨 있다.
- 헤더(Header) : 헤더 정보(Host, Content-Type 등)를 담고 있다.
- 바디(Body) : form 파라미터 형식, message body 등을 담고 있다.

HttpServletRequest 객체는 HTTP 메시지 파싱 뿐만 아니라 여러가지 부가기능도 함께 제공한다.

**임시 저장소 기능**

HTTP 요청의 시작부터 끝날 때 까지 유지되는 임시 저장소 기능의 메서드를 제공하고 있다.

저장 : setAttribute(name, value)

조회 : getAttribute(name)

**세션 관리 기능**

getSession(create: true) : 세션을 유지할 수 있도록 기능을 제공한다.

## HTTP 요청 데이터

HTTP 요청 메시지를 통해 클라이언트에서 서버로 데이터를 전달하는데에는 여러 가지 방법이 있다.

주로 GET, POST와 HTTP message body에 데이터를 직접 담아서 요청하는 방법을 사용한다.

**GET - 쿼리 파라미터**

- 메시지 바디 없이, URL에 쿼리 파라미터에 데이터를 포함해서 전달하는 방식이다.
- https://localhost:8080/member**?username=kim&age=20**
- 검색, 필터, 페이징 등에서 주로 사용한다.

**POST - HTML Form**

- 메시지 바디에 쿼리 파라미터 형식으로 전달하는 방식이다.
- 메시지 바디 : username=kim&age=20
- content-type: application/x-www-form-urlencoded
- 회원 가입, 상품 주문, HTML Form 등에서 주로 사용한다.

**HTTP message body에 데이터를 직점 담아서 요청**

- HTTP API, REST API 등에서 주로 사용된다.
- JSON, XML, TEXT 형식으로 보낼 수 있다. 대부분 JSON 포맷을 사용한다.
- POST, PUT, PATCH 메서드에 사용된다.

## HttpServletRequest 사용

HttpServletRequest가 제공하는 기본 기능들은 매우 다양하다.

아래 코드는 HttpServerletRequest가 제공하는 메서드들을 통해서 HTTP 메시지의 start line, header, 기타 정보 등을 조회하는 예제이다.

```java
@WebServlet(name = "requestHeaderServlet", urlPatterns = "/request-header")
public class RequestHeaderServlet extends HttpServlet {

    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        printStartLine(request);
        printHeaders(request);
        printHeaderUtils(request);
        printEtc(request);
    }

		// start line 정보 조회
    private static void printStartLine(HttpServletRequest request) {
        System.out.println("--- REQUEST-LINE - start ---");
        System.out.println("request.getMethod() = " + request.getMethod());
        System.out.println("request.getProtocol() = " + request.getProtocol());
        System.out.println("request.getScheme() = " + request.getScheme());
        System.out.println("request.getRequestURL() = " + request.getRequestURL());
        System.out.println("request.getRequestURI() = " + request.getRequestURI());
        System.out.println("request.getQueryString() = " + request.getQueryString());
        System.out.println("request.isSecure() = " + request.isSecure());
        System.out.println("--- REQUEST-LINE - end ---");
        System.out.println();
    }

		// 헤더 정보
    private void printHeaders(HttpServletRequest request) {
        System.out.println("--- Headers - start ---");

        request.getHeaderNames().asIterator()
                .forEachRemaining(headerName -> System.out.println(headerName + ":" + request.getHeader(headerName)));

        // 헤더 정보를 1개씩 꺼내는 방법
        System.out.println(request.getHeader("host"));

        System.out.println("--- Headers - end ---");
        System.out.println();
    }

    // Header 편리한 조회
    private void printHeaderUtils(HttpServletRequest request) {
        System.out.println("--- Header 편의 조회 start ---");
        System.out.println("[Host 편의 조회]");
        System.out.println("request.getServerName() = " + request.getServerName()); //Host 헤더
        System.out.println("request.getServerPort() = " + request.getServerPort()); //Host 헤더
        System.out.println();

        System.out.println("[Accept-Language 편의 조회]");
        request.getLocales().asIterator()
                .forEachRemaining(locale -> System.out.println("locale = " + locale));
        System.out.println("request.getLocale() = " + request.getLocale());
        System.out.println();

        System.out.println("[cookie 편의 조회]");
        if (request.getCookies() != null) {
            for (Cookie cookie : request.getCookies()) {
                System.out.println(cookie.getName() + ": " + cookie.getValue());
            }
        }
        System.out.println();

        System.out.println("[Content 편의 조회]");
        System.out.println("request.getContentType() = " + request.getContentType());
        System.out.println("request.getContentLength() = " + request.getContentLength());
        System.out.println("request.getCharacterEncoding() = " + request.getCharacterEncoding());
        System.out.println("--- Header 편의 조회 end ---");
        System.out.println();
    }

		// 기타 정보
    private void printEtc(HttpServletRequest request) {
        System.out.println("--- 기타 조회 start ---");
        System.out.println("[Remote 정보]");
        System.out.println("request.getRemoteHost() = " + request.getRemoteHost());
        System.out.println("request.getRemoteAddr() = " + request.getRemoteAddr());
        System.out.println("request.getRemotePort() = " + request.getRemotePort());
        System.out.println();

        System.out.println("[Local 정보]");
        System.out.println("request.getLocalName() = " + request.getLocalName());
        System.out.println("request.getLocalAddr() = " + request.getLocalAddr());
        System.out.println("request.getLocalPort() = " + request.getLocalPort());
        System.out.println("--- 기타 조회 end ---");
        System.out.println();
    }
}
```

HTTP 메시지의 원하는 부분을 HttpServerletRequest가 제공하는 메서드를 통해 쉽게 조회할 수 있다.