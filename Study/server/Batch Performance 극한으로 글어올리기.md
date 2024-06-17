<iframe width="560" height="315" src="https://www.youtube.com/embed/L9K0l65wMbQ?si=GQeSkQjhdqPmg-VT" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- [i] Batch Applicaiton: `일괄처리`
	- 특정 시간에 많은 데이터를 일괄 처리.
	- 서버개발자들은 배치 방식이 real-time service에 비해 상대적으로 *개발 부담이 적다고 생각하는 경향이 있다.*

> [!summary] 크게 3가지 Batch로 개발하는 경우
> 1. **일괄 생성**(READ -> CREATE -> WRITE)
> 2. **일괄 수정**(READ -> UPDATE -> WRITE)
> 3. **통계** (SUM READ -> CREATE -> WRITE)

> [!warning] 하지만, Batch Performance에 큰 신경은 쓰지 않는다.
> Batch개발을 쉽게 생각하는 경향, 배포 후 관리 소홀, 배치를 원하는 APM Tool의 부재

# Batch 성능 개선의 첫걸음 = Reader개선
대부분 Batch성능에서 차지하는 비중은 Writer보다 `Reader`가 높다.
- 대표적인 사례로 RDBMS에서 SELECT Query를 튜닝하는 것 만으로도 Batch Performance는 극적으로 개선된다.

## Batch에서 Data를 읽는 절대적인 방법 => Chunk Processing
대량 Batch Processing은 항상 chunkProcessing을 이용할 수 밖에 없다.
- 천만개의 데이터를 한번에 가져와 처리할 수 있는 애플리케이션은 사실상 없다.

## Chunk Processing의 짝꿍으로 Pagination Reader를 사용하게 된다.
데이터를 한번에 받는것이 아닌, page단위로 받기 위함
대표적으로 `JpaPagingItemReader`, `RepositoryItemReader`가 있음

- [!] 그러나 이런 방식은 대량 처리에 매우 부적합하다.
      Limit offset이 가진 태생적인 한계 때문이다.

```sql
--category에 index가 있다는 전재 하에
SELECT * FROM orders WHERE category = 'Book' LIMIT 0, 1000;
-- 아직까지는 매우 빠르지만,
SELECT * FROM orders WHERE category = 'Book' LIMIT 50000000, 1000;
-- Offset이 커질수록 매우 느려진다.
```

- [I] 이런 문제를 해결한 `ZeroOffsetItemReader`
- 항상 offset을 0으로 유지한다.
```SQL
SELECT * FROM orders WHERE category = 'Book' and id > 0 limit 0, 1000;

SELECT * FROM orders WHERE category = 'Book' and id > 9676800 lmit 0 , 1000;
```

- [?] 예시는 autoIncrement기준인데, db에 종속적이지 않은 id를 사용한다면 이 부분을 고려하여 설계해야 할 것으로 생각됨
+ QueryDsl을 결합

```kotlin
QuerydslZeroOffsetItemReader(
  name = "orderQueryDslZeroOffsetItemReader",
  pageSize = 1000,
  entityManagerFactory = entityManagerFactory,
  idAndSort = Asc,
  idField = qOrder.id
){
  it.from(qOrder)
	  .innerJoin(qOrder.customer).fetchJoin()
	  .select(qOrder)
	  .where(qOrder.category.eq(CATEGORY.BOOK))
}
```

# 데이터를 조금씩 가져오는 Cursor를 사용하자!
mysql Cursor는 데이터가 없을때 까지, 일정 갯수를 반복해서 제공한다. 그렇기때문에 chunk processing에 잘 어울리는 방식임

## Spring에서 cursor를 지원하는 itemReader

- [c] **JpaCursorItemReader**
	MySQL Cursor 방식 ❌
	데이터를 모두 읽고 서버에서 직접 Cursor하는 방식 -> OOM유발
 - [p] **JdbcCursoritemReader**
	 MySQL Curosr 방식 ⭕️
	 MySQL의 Curosr를 사용하여 일정 개수만큼 Fetch하는 방식
	 - 그러나, HQL이나 Native Query를 사용해야한다. (문자열 방식의 구현)

> Kotlin기반 ORM프레임 워크인 `Exposed`사용
> - 데이터베이스 Acess 방식
> 	SQL을 매핑한 DSL 방식, 경량화한 ORM DAO방식
> - kotlin 호환(단, 자바 프로젝트는 사용 불가)

### Exposed DSL
Exposed DSL을 사용하면 Kotlin의 언어적 특성을 활용하여 쿼리 구현이 가능하다.
```kotlin
object Orders: LongIdTable("orders"){
  val customer = reference("customer_id", Customers).nulla
}
```