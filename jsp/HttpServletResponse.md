## Intro

JSP 라이브러리에서는 HTTP 메시지를 편리하게 조회하고 사용할 수 있도록 도와주는 HttpServletRequest, HttpServletResponse 객체를 제공하고 있다.

## HttpServletResponse

HTTP 응답 메시지를 개발자가 직접 생성해도 되지만 매우 번거롭다.

서블릿(Servlet)은 개발자가 HTTP 응답 메시지를 편리하게 사용할 수 있도록 생성해 준다.

HttpServletResponse는 HTTP 응답 메시지를 생성하는 역할을 한다.

**HTTP 응답 메시지 생성**

- HTTP 응답 코드 지정(1xx, 2xx, 3xx, 4xx, 5xx)
- 헤더 생성
- 바디 생성

**편의 기능**

- Content-Type 편리하게 지정
- 쿠키의 편리한 생성
- Redirect 기능

## HttpServletResponse 사용

```java
@WebServlet(name = "responseHeaderServlet", urlPatterns = "/response-header")
public class ResponseHeaderServlet extends HttpServlet {

    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // [status-line]
        response.setStatus(HttpServletResponse.SC_OK);

        // [response-headers]
        response.setHeader("Content-Type", "text/plain;charset=utf-8");
        response.setHeader("Cache-Control", "no-cache, no-store, must-revalidate");
        response.setHeader("Pragma", "no-cache");
        response.setHeader("my-header", "hello");

        // [Header 편의 메서드]
        content(response);
        cookie(response);
        redirect(response);

        // [message body]
        PrintWriter writer = response.getWriter();
        writer.print("ok");
    }

    private void content(HttpServletResponse response) {
        // Content-Type: text/plain;charset=utf-8
        // Content-Length: 2

        // response.setHeader("Content-Type", "text/plain;charset=utf-8");
        response.setContentType("text/plain");
        response.setCharacterEncoding("utf-8");
        // response.setContentLength(2); //(생략시 자동 생성)
    }

    private void cookie(HttpServletResponse response) {
        // Set-Cookie: myCookie=good; Max-Age=600;
        // response.setHeader("Set-Cookie", "myCookie=good; Max-Age=600");

        Cookie cookie = new Cookie("myCookie", "good");
        cookie.setMaxAge(600); //600초
        response.addCookie(cookie);
    }

    private void redirect(HttpServletResponse response) throws IOException {
        // Status Code 302
        // Location: /basic/hello-form.html

        // response.setStatus(HttpServletResponse.SC_FOUND); //302
        // response.setHeader("Location", "/basic/hello-form.html");
        response.sendRedirect("/basic/hello-form.html");
    }
}
```