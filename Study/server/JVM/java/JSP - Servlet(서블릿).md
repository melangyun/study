# Servlet(서블릿)

> 클라이언트 요청을 처리하고, 그 결과를 반환하는 Servlet클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술

좀 더 들어가서 설명하면 클라이언트가 어떠한 요청을 하면 그에 대한 결과를 다시 전송해 주어야 하는데, 이러한 역할을 하는 자바 프로그램
- 서블릿은 자바로 구현된 CGI라고 흔히 이야기한다.

**서블릿 특징**
- 클라이언트 요청에 대해 동적으로 작동하는 웹 어플리케이션 컴포넌트
- html을 사용하여 요청에 응답
- Java Thread를 이용하여 동작
- MVC패턴에서 Controller로 이용된다.
- HTTP 프로토콜 서비스를 지원하는 javax.servlet.http.HttpServlet 클래스를 상속받는다
- UDP보다 처리 속도가 느리다.
- HTML변경시 Servlet을 재 컴파일해야 하는 단점이 있다.

일반적으로 웹서버는 정적인 페이지만을 제공한다. 그렇기 때문에 동적인 페이지를 제공하기 위해 웹 서버는 다른 곳에 도움을 요청하여 동적인 페이지를 작성한다. 동적인 페이지로는 임의의 이미지만을 보여주는 페이지와 같이 사용자가 요청한 시점에 페이지를 생성해서 전달해 주는것을 의미.


![servlet Container](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F993A7F335A04179D20)
1. 사용자(클라이언트)가 URL을 입력하면 HTTP Request가 Servlet Container로 전송한다.
2. 요청을 전송받은 Servlet Container는 HttpServletRequest, HttpServletResponse객체를 생성
3. web.xml을 기반으로 사용자가 요청한 URL이 어느 서블릿에 대한 요청인지 찾는다.
4. 해당 서블릿에서 service메소드를 호출 한 후 클라이언트의 Get,Post 여부에 따라 `doGet()`또는 `doPost()`를 호출
5. `doGet()`or `doPost()` 메소드는 동적 페이지를 생성한 후 HttpServletResponse객체에 응답을 보낸다.
6. 응답이 끝나면 `HttpServletRequest`, `HttpServletResponse`두 객체를 소멸

# Servlet Container (서블릿 컨테이너)
> 서블릿을 관리해주는 컨테이너

서블릿을 만들었다고 해서 스스로 동작하는것이 아니라, 서블릿을 관리해 주는것이 필요한데, 그 역할을 하는것이 서블릿 컨테이너.
서블릿이 어떠한 역할을 수행하는 정의서라고 보면, 서블릿 컨테이너는 그 정의서를 보고 수행한다고 볼 수 있다. 서블릿 컨테이너는 `클라이언트의 요청(Request)을 받아주고 응답(Response)을 할 수 있게, 웹 서버와 소켓으로 통신`하며 대표적인 예로 *톰캣*이 있다.
톰캣은 실제로 웹 서버와 통신하여 JSP(자바 서버 페이지)와 Servlet이 작동하는 환경을 제공해준다.

## Servlet 생명 주기
![서블릿 생명 주기](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F991870335A04292F0B)

1. 클라이언트의 요청이 들어오면 컨테이너는 ==해당 서블릿이 메모리에 있는지 확인. 없을 경우 `init()`메소드를 호출==하여 적재
	- init() 메소드는 처음 한번만 실행되기 때문에, 서블릿의 쓰레드에서 공통적으로 사용해야하는것이 있다면 오버라이딩하여 구현하면 된다.
	- 실행 중 서블릿이 변경될 경우 기존 서블릿을 파괴하고 init()을 통해 새로운 내용을 다시 메모리에 적재
2.  `init()`이 호출된 후 클라이언트의 요청에 따라서 service()메서드를 통해 요청에 대한 응답이 doGet(), doPost로 분기
	   이때 서블릿 컨테이너가 클라이언트의 요청이 오면 가장 먼저 처리하는 과정으로 생성된 `HttpServletRequest`, `HttpServletResponse`에 의해 request와 response객체가 제공된다.
   3. 컨테이너가 서블릿에 종료 요청을 하면 `destory()`메서드가 호출. 한번만 실행되며, 종료시에 처리해야 하는 작업들은 `destroty()`메서드를 오버라이딩 하여 구현하면 된다.

# 3. JSP(JavaServerPage)
> Java 코드가 들어있는 HTML코드

서블릿은 자바 소스코드 속에서 HTML 코드가 들어가는 형태인데, JSP는 이와 반대로 HTML 소스 코드 속에 자바 소스코드가 들어가는 구조이다.



---
[JSP 서블릿이란?](https://mangkyu.tistory.com/14)