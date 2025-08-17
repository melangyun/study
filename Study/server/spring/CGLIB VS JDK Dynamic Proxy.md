> [!example] proxy의 사용
> 스프링에서 `@JobScope`, `@StepScope`, `@RequestScope` 같은 <u>스코프 빈</u>은  요청 시점 / 잡 실행 시점에 만들어지는 객체
> ==그런데, Spring은 컨테이너 초기화할 때 이미 "필드주입"을 해줘야한다==
> - 그래서 진짜 객체 대힌 대리 객체 (프록시)를 먼저 주입해둔다.
> - 이 프록시가 나중에 실제 객체를 대신 찾아서 호출해준다.

CGLIB(Code Generation Library) 바이트코드를 조작해서 클래스의 서브 클래스를 동적으로 생성하는 라이브러리

> 스프링에서 프롤시를 만들 때 `JDK Dynamic Proxy`와 `CGLIB` 두 가지 방식을 쓴다.
- JDK Dynamic Proxy -> 인터페이스 기반 (인터페이스가 있어야 가능) 
- CGLIB -> 클래스 상속 기반 (클래스를 상속 받아 프록시 생성)

1. JDK Dynamic Proxy
	- 인터페이스 기반.
	- 인터페이스를 구현하는 `대리객체`를 만듬
	- 자바 기본 제공 리플렉션 API (java.lang.reflect.Proxy)로 동작
	- [k] 인터페이스가 반드시 필요! 
2. CGLIB (Code Generation Library)
	- 클래스 상속 기반
	- 대상 클래스를 상속해서 `가짜 자식 클래스`를 만듬
	- [k] 인터페이스 없어도 됨
	- [k] 상속 불가능한 클래스 /  메서드는 사용하지 못함


# Scope annotaion
스코프 애노테이션은 내부적으로 클래스 기반 프록시를 기본 값으로 갖고있다.
```java
@Scope(value = "job", proxyMode = ScopedProxyMode.TARGET_CLASS)
```
그래서 CGLIB 기반 프록시가 생성되고, 해당 빈은 실제 객체 대신 CGLIB이 만든 자식 클래스가 컨테이너에 들어가게 된다.

> [!question] 그럼 JDK Dynamic Proxy는 어디에 쓰일까?
# 1. Spring AOP
- `@Transactional`, `@Async`, `@Cacheable`같은 어노테이션
- 대상 객체가 인터페이스를 구현하고 있다면 JDK Dynamic Proxy방식으로 프록시 생성
- 대상 객체가 인터페이스가 없다면 CGLIB 사용
```java
public interface MemberService {
    void saveMember();
}

@Service
public class MemberServiceImpl implements MemberService {
    @Override
    public void saveMember() { ... }
}
```
`@Transactional` 이 클래스에 붙으면 스프링이 프록시 객체를 컨테이너에 등록한다
즉, `MemberServiceImpl`대신 Proxy(JDK Dynamic Proxy)가 들어가고, 그 Proxy가 내부에서는 MemberServiceImpl에게 위임한다.

# 2. Spring Data JPA Repository
- JpaRepository, CrudRepository
- ==실제 구현체는 없는데, 스프링이 JDK Dynamic Proxy로 프록시 객체를 만들어 대신 실행로직 (SimpleJpaRepository)로 연결해줌==
# 3. FeignClient
- 내부적으로 JDK Dynamic Proxy를 활용해 인터페이스 호출 -> 실제 HTTP 호출로 위임

