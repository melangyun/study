Spring Batch의 핵심은 Step이고, Step은 두 가지 스타일로 작성할 수 있다.
- 청크 지향 처리 (Chunk-oriented Processing)
- Tasklet 지향 처리 (Tasklet-oriented Processing)
# 1. 청크 지향 처리 (Chunk-oriented Processing)

- 대량 데이터 처리에 최적화된 방식
- 하나의 Step이 Reader → Processor → Writer 구조로 동작 
- 데이터를 한 건 씩 읽고, 모아서, 한번에 쓰기 때문에 성능과 안정성이 높다.
- **트랜잭션 단위는 청크 단위이다**

# 2. Tasklet 지향 처리(Tasklet-oriented Processing)
- step이 단순이 *하나의 태스크*만 수행
- Tasklet은 `RepeatStatus.FINISHED`를 리턴하면 종료한다.
- 데이터를 대량으로 처리하기보단, 작은 단위 작업(파일 이동, API 호출, 로그 정리, 단일 계산)등에 적합
- 트랜잭션 단위 → Step 전체 (필요 시 Tasklet 내부에서 직접 제어 가능)
- [w] 보통은 데이터 읽기/ 쓰기보단 한번의 실행으로 끝나는 로직에 사용한다.
	ex) 특정 테이블 초기화, 파일 압축/전송, 외부 시스템 API 호출 등

| 구분          | 청크지향(Chunk)                                 | Tasklet지향(Tasklet)                       |
| ------------- | ----------------------------------------------- | ------------------------------------------ |
| 처리대상      | 대량 데이터(DB, 파일, MQ 등)                    | 단순 / 단일 테스크                         |
| 구조          | Reader → Processor → Writer                     | Tasklet 구현체 하나                        |
| 트랜잭션 단위 | 청크단위                                        | Step 전체 or<br>Tasklet 내부에서 수동 처리 |
| 장점          | 대용량 데이터 안정적 처리<br>롤백 / 재시도 용이 | 구현 단순<br>단일 작업에 적합              |
| 사용 예시     | 100만건 DB조회 후 파일로 저장                   | 로그 파일 삭제, 외부 API 호출              |
