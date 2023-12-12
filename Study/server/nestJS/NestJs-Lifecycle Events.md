# Lifecycle Events

모든 응용 프로그램 요소에는 Nest에서 관리하는 수명주기가 있다.
Nest는 **수명 후크**를 제공하여 주요 수명 순간에 대한 가시성과 발생시 행동 할 수있는 기능을 제공한다.

## Lifecycle sequence

생성자를 호출하여 인젝터블/컨트롤러를 생성한 후 Nest는 특정 순간에 다음 순서로 라이프 사이클 후크 메소드를 호출한다.

| Lifecycle hook method   | Lifecycle event trigger the hook method call                                              |
| ----------------------- | --------------------------------------------------- |
| OnModuleInit            | 호스트 모듈이 초기화되면 호출                       |
| On ApplicationBootstrap | 응용 프로그램이 완전히 시작되고 부트스트랩되면 호출 |
| OnModuleDestroy         | Nest가 호스트 모듈을 파괴하기 직전에 정리           |
| OnApplicationShutdown   | 시스템 신호에 응답                                  |


# RequestLifecycle

- Request에 사용자 정보가 있어서 컨트롤러 전에서 검증(jwt)
- Request 자체 데이터 타입을 검증(pipe)
- response를 줄 때, 내가 원하는 response로 변경하여 반환
- 에러 핸들링(Exception filter)

## 요청 생명주기

1. Incoming request
2. Globally bound middleware
3. Module bound middleware
4. Global guards
5. Controller guards
6. Route  
7. Global interceptors (pre-controller)
8. Controller interceptors (pre-controller)
9. Route interceptors (pre-controller)
10. Global pipes
11. Controller pipes
12. Route pipes
13. Route parameter pipes
14. Controller (method handler)
15. Service (if exists)
16. Route interceptor (post-request)
17. Controller interceptor (post-request)
18. Global interceptor (post-request)
19. Exception filters (route, then controller, then global)
20. Server response

![nestjs request flow](https://velog.velcdn.com/images%2Fharon%2Fpost%2Fe2587453-9aa2-4f2d-9ae4-0c8c024ed42f%2Fimage.png)



---
[\[NestJS\] Lifecycle Events](https://velog.io/@haron/NestJS-Lifecycle-Events)
[Lifecycle Events](https://jakekwak.gitbook.io/nestjs/fundamentals/lifecycle-events)