> [!question] PlatformTransactionManager란?
> Spring에서 트랜잭션을 추상화한 최상위 인터페이스
> JDBC, JPA, JMS, Hibernate, Mongo 등 트랜잭션 대상 리소스는 모두 다른데, 스프링은 PlatformTransactionManager 인터페이스로 감싸서 일관되게 트랜잭션을 제어할 수 있게 해준다.

**주요 구현체**
- DataSourceTransactionManager (JDBC 기반)
- JpaTranssactonManager (JPA EntityManager 기반)
- JtaTransactionManager (분산 트랜잭션)
- ResourcelessTransactonManager (실제 리소스 없는 가짜 트랜잭션)

> 즉, PlatformTransactionManager는 트랜잭션 매니저들의 공통 부모 인터페이스이고, 스프링은 이걸 통해 `@Transactional`을 추상적으로 처리

---
> [!warning] Spring Batch에서 내부적으로 두 가지 다른 목적의 트랜잭션을 사용한다.
> 1. 메타 데이터 관리용 트랜잭션
> 	- Batch가 JobRepository테이블에 JobExecution, StepExecution, 상태 / 재시도 이력 등을 기록하는데, 이 기록 자체도 트랜잭션을 걸고 DB에 커밋
> 	- 여기에는 보통 DataSourceTransactionManager가 쓰임
> 2. 비즈니스 로직용 트랜잭션
> 	- Step안의 Reader/ Processor/Writer 또는 Tasklet에서 실행되는 사용자 로직에 트랜잭션을 적용할 수도 있다.
> 	- 이부분은 DB를 안쓴다면 ResourcelessTransacitonManager같은걸 붙일수도 있음
> 
> - [!] 만일 PlatformTransactionManager를 Bean으로 딱 하나만 정의해두면, 메타데이터 관리에도 같은 메니저를 써버리기 때문에, 배치 실행 메타데이터가 롤백되거나, 커밋 타이밍이 꼬이는 등 의도치 않은 문제가 생긴다.

따라서 PlatfromTransactionManager는 한 종류가 아니라 여러 개를 따로 등록해서 상황별로 써야 한다는것이 핵심.


