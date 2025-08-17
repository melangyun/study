>[!question] 왜 쓰는가?
>- job /step 실행시점에만 Bean을 만들고 싶을때.

기본작으로 Spring Bean은 컨테이너 초기화 시점에 만들어진다. 그런데 Batch에서는 Job 실행할 때마다 달라지는 JobParameter, StepExecutionContext같은 값이 있는데, 이걸 애플리케이션 시작시 주입받는건 불가능
- 그래서 Bean생성을 Job실행 시점/ Step 실행 시점으로 미루기 위해 스코프를 검

```kotlin
@Bean
@StepScope
fun reader(
    @Value("#{jobParameters['filePath']}") filePath: String
): FlatFileItemReader<MyEntity> {
    return FlatFileItemReaderBuilder<MyEntity>()
        .name("myReader")
        .resource(FileSystemResource(filePath))
        .delimited()
        .names("id", "name")
        .targetType(MyEntity::class.java)
        .build()
}
```

또한 Batch는 멀티 스레드 / 파티셔닝 / 멀티스텝 시나리오가 존재하는데, Reader / Writer 컴포넌트를 싱글톤 Bean으로 두면 동시성 문제가 발생 가능한다.
`@StepScope` 로 선언하면 Step 실행마다 새로운 인스턴스가 만들어져서 안전하다.

# JobScope, Step Scope 사용시 주의사항
1. 프록시 대상의 타입이 클래스인 경우 반드시 상속 가능한 클래스여야 한다.
    CGLIB를 사용해 클래스 기반 프록시를 생성하고, 대상 클래스가 상속가능해야 한다.
    - [[CGLIB VS JDK Dynamic Proxy]]
2. Step빈에는 @StepScope 사용 x
	- Step 빈 생성과 스코프 활성화 시점이 맞지 않아 오류가 발생한다.
	- Spring Batch는 Step 실행 전 메타데이터 관리를 위해 Step 빈에 접근해야 한다.
	  그러나 Step이 실행되지 않아, `@StepScope`가 활성화 되지 않았고, 결국 스코프가 활성화 되지 않은 상태에서 프록시에 접근하려니 잘못된 접근이 되는것
3. Step 빈에도 `@JobScope` 사용 권장 x
```java
@Bean
@JobScope  // Step에 @JobScope를 달았다
public Step systemDestructionStep(
   @Value("#{jobParameters['targetSystem']}") String targetSystem
) {
   return new StepBuilder("systemDestructionStep", jobRepository)
       .tasklet((contribution, chunkContext) -> {
           log.info("{} 시스템 침투 시작", targetSystem);
           return RepeatStatus.FINISHED;
       }, transactionManager)
       .build();
}
```
만약 여기서 Step에서 `@JobScope`를 제거하면 targetSystem 파라미터를 받을 수 없다. 그럼 어떻게 해야할까?
```java
@Bean
public Step systemDestructionStep(
    SystemInfiltrationTasklet tasklet  // Tasklet을 주입받는다
) {
    return new StepBuilder("systemDestructionStep", jobRepository)
        .tasklet(tasklet, transactionManager)
        .build();
}

@Slf4j
@Component
@StepScope  // Tasklet에 @StepScope를 달았다
public class SystemInfiltrationTasklet implements Tasklet {
    private final String targetSystem;

    public SystemInfiltrationTasklet(
        @Value("#{jobParameters['targetSystem']}") String targetSystem
    ) {
        this.targetSystem = targetSystem;
    }

    @Override
    public RepeatStatus execute(StepContribution contribution, ChunkContext context) {
        log.info("{} 시스템 침투 시작", targetSystem);
        return RepeatStatus.FINISHED;
    }
}
```
