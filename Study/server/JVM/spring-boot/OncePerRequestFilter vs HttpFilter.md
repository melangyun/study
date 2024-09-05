# OncePerRequestFilter
스프링 프레임워크에서 제공하는 클래스
`특정 요청마다 한번만 실행되는 것을 보장.`
- 동작방식
	- 각 HTTP 요청에 대해 한 번만 실행.
	  이는 여러번의 내부 포워드(forward)나 인클루드(include) 시에도 필터가 다시 실행되지 않도록 한다.
	- 주로 보안, 로깅 등의 목적에서 요청 당 한 번만 처리해야 하는 로직을 구현할 때 사용된다.
	- doFilterInternal 메서드를 오버라이드 하여 필터링 로직을 구현한다.

```java
public class MyOncePerRequestFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
            throws ServletException, IOException {
        // 필터링 로직
        filterChain.doFilter(request, response);
    }
}
```


# HttpFilter
[[JSP - Servlet(서블릿)]]에서 제공하는 클래스
`서블릿 API의 Java.servlet.Filter`인터페이스를 구현한 필터. 모든 HTTP요청을 필터링 할 수 있다.

- 동작 방식
	- 모든 HTTP 요청을 처리하며, 여러번의 내부 포워드(forward)나 인클루드(include)가 발생할 때 마다 실행될 수 있다.
	- doFilter 메서드를 오버라이드하여 필터링 로직을 구현한다.
	- HTTP에 특화된 기능을 제공하며 HttpServletRequest와 HttpServletResponse를 직접 사용할 수 있다.

```java
public class MyHttpFilter extends HttpFilter {
    @Override
    protected void doFilter(HttpServletRequest request, HttpServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        // 필터링 로직
        chain.doFilter(request, response);
    }
}
```


# 주요 차이점
- 실행 횟수
	- OncePerRequestFilter: 요청당 한번만 실행된다.
	- HttpFilter: 요청이 처리되는 동안 여러번 실행될 수 있다.
- 사용 목적
	- OncePerRequestRilter: 보안, 로깅 등 특정 요청마다 한 번만 실행되어야 하는 경우 유용
	- HttpFilter: 일반적인 HTTP 요청에 유용. HTTP 요청 및 응답을 직접 다룰 수 있다.