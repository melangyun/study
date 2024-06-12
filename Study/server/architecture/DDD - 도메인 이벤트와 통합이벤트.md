도메인 이벤트는 메시징 스타일 이벤트와 유사하지만 한가지 중요한 차이점이 있다.
- **실제 메시지**, 메시지 큐, 메시지 broker 또는 AMQ를 사용하는 서비스 버스에서 메시지는 항상 비동기식으로 전송되고 프로세스와 머신에서 통신된다.
	- [I] 다수의 바인딩된 컨텍스트, 마이크로 서비스 또는 다른 애플리케이션을 통합하는데 유용하다.
- **도메인 이벤트**  는 거의 즉시, 프로세스 내에서, 동일한 도메인 내에서 발생해야 한다.
  도메인 이벤트는 <u>동기 또는 비동기일 수 있다.</u>
	  - IoC컨테이너 혹은 다른 메서드를 기반으로 메모리 내 중재자로 구현될 수 있는 도메인 이벤트 디스패처에 푸시되는 메시지이다.

## 통합이벤트

통합 이벤트는, 커밋된 트랜잭션 및 업데이트를 다른 마이크로 서비스, 바인딩 된 컨텍스트 또는 외부 어플리케이션과 같은 추가적인 하위 시스템에 전파하는것이다.
따라서 엔티티가 성공적으로 지속되고 있는 경우에만 발생해야 하며, 그렇지 않으면 전체 작업이 발생하지 않은 것 처럼 처리된다.

통합 이벤트는 여러 마이크로 서비스(기타 바인딩된 컨텍스트) 또는 외부 시스템 / 애플리케이션 간에도 비동기 통신을 기반으로 해야한다.

도메인 이벤트는동일한 도메인 내의 여러 Aggregate에 파생작업을 트리거한다.

![도메인 이벤트](https://learn.microsoft.com/ko-kr/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/media/domain-events-design-implementation/domain-model-ordering-microservice.png)
애그리거트의 하위 엔티티(위 예시의 `OrderItem`)도메인 이벤트를 발행시킬 수 있다. 예를 들어 각 OrderItme 하위 엔터티는 가격이 기준보다 너무 높을때 이벤트를 발행할 수 있다.

도메인 이벤트 처리는애플리케이션 레이어의 문제이며, 도메인 계층은 도메인 논리에만 집중해야한다. 따라서 애플리케이션 레이어에 도메인 이벤트 리스너가 존재해야한다.

도메인 이벤트는 listener을 계속해서 늘릴수 있다는것에 초점이 맞춰진다.  어떤 일이 발생했을 때 부수적으로 발생하는 액션이 추가된다면 OCP와 SOLID, SRP에 위배된다.

![도메인 이벤트 발행!](https://learn.microsoft.com/en-us/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/media/domain-events-design-implementation/aggregate-domain-event-handlers.png)


# Single transaction across aggregates versus eventual consistency across aggragates :애그리 거트간 단일 트랜잭션 및 최종 일관성

에릭 에반스와 본 버논과 같은 많은 DDD저자는 하나의 트랜잭션 = 하나의 애그리거트라는 규칙을 옹호하므로, 애그리거트 간 최종 일관성을 주장한다.

> 하나의 애그리거트 인스턴스에서 명령을 실행하려면 하나 이상의 애그리거트에서 추가 비즈니스 규칙을 실행해야 하는 최종 일관성을 사용한다.







---
[도메인 이벤트: 디자인 및 구현](https://learn.microsoft.com/en-us/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/domain-events-design-implementation)