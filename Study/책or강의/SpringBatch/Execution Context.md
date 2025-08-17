Job / Step 실행 도중 중간 상태나 메타데이터를 안전하게 저장 - 복원할 수 있는 컨테이너
- JobExecution과 StepExecution에 붙어있는 Key-Value 저장소
- 배치 실행 중간에 필요한 커스텀 데이터 (마지막 인덱스, 상태, 중간 결과 등)를 보존하는 용도로 사용
- Job/Step이 재시작 될 때, 저장된 ExecutionContext 덕분에 "중단된 지점부터 이어서 실행"이 가능

**예시**
Reader에서 파일 처리하다가 인덱스 1000에서 실패 → 재시작하면 인덱스 1000부터 이어서 실행하고 싶음.
- [l] 이때 “마지막 처리 인덱스”를 ExecutionContext 에 저장해둔다.

**JobScope/ StepScope Bean에서 접근하기**
@JobScope, @StepScope 빈 안에서 @Value 표현식으로 ExecutionContext 값 주입이 가능하다
```java
@Bean
@JobScope
public Tasklet systemDestructionTasklet(
    @Value("#{jobExecutionContext['previousSystemState']}") String prevState
) {
    return (contribution, chunkContext) -> {
        // JobExecutionContext에서 이전 시스템 상태를 읽음
        return RepeatStatus.FINISHED;
    };
}

@Bean
@StepScope
public Tasklet infiltrationTasklet(
    @Value("#{stepExecutionContext['targetSystemStatus']}") String targetStatus
) {
    return (contribution, chunkContext) -> {
        // StepExecutionContext에서 타겟 시스템 상태를 읽음
        return RepeatStatus.FINISHED;
    };
}

/*
- jobExecutionContext[...] : Job 레벨 공유 컨텍스트
- stepExecutionContext[...] : Step 레벨 컨텍스트 (해당 Step 안에서만 유효)
*/
```

- **JobExecutionContext**
	- 하나의 Job 전체에서 공유됨.
    - 즉, 모든 Step에서 @Value("#{jobExecutionContext['key']}") 로 접근 가능.
-  **StepExecutionContext**
    - 특정 Step 안에서만 접근 가능.
    - 다른 Step에서는 해당 StepExecutionContext 값을 직접 가져올 수 없음.
