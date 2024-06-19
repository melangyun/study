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
- <mark style="background: #D2B3FFA6;">천만개의 데이터를 한번에 가져와 처리할 수 있는 애플리케이션은 사실상 없다.
</mark>

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
> - 왠만한 RDBMS는 모두 지원
> - kotlin 호환(단, 자바 프로젝트는 사용 불가)

### Exposed DSL
Exposed DSL을 사용하면 Kotlin의 언어적 특성을 활용하여 쿼리 구현이 가능하다.
```kotlin
object Orders: LongIdTable("orders"){
  val customer = reference("customer_id", Customers).nullable()
  val name = varchar("name", 50)
  val price = varchar("name", 50).default(0)
  val category = varchar("category", 50)
  val deliveryCompleted = bool("is_delivery_completed")
}

object Customers: LongIdTable("customer"){
  val name = varchar("name", 20)
  val email = varchar("email", 50)
  val age = long("age")
}
```

```kotlin
// Select
Customers.slice(Customers.name)
  .select { age eq 25}

// Insert
Customers.insert{
  customers -> 
		  customers[name] = "홍길동"
		  customers[email] = "@kakao.com"
		  customers[age] = 25
}

// Batch Insert
Customers.batchInsert(data = items) { item ->
  this[Customers.name] = item.name
  this[Customers.email] = item.email
  this[Customers.age] = item.age
}
```
- 동작 방식 = `jdbcCursorItemReader`
- 쿼리 = `Exposed DSL`
	- 성능과 관련해서 Exposed DSL이 필수는 아니지만, 개발자의 생산성을 크게 향상시켜줄 수 있다.
```kotlin
ExposedCursorItemReader<Order>(
  name = "orderExposedCursorItemReader",
  dataSource = dataSource,
  fetchSize = 5000
){
  (Orders innerJoin Customers)
    .slice(Orders.columns)
    .select{
      (Orders.category eq "Book") and
	      (Customers.age greaterEq 11)
    }
}
```

카카오 페이 기존

|                |   RepositoryItemReader<br/>JpaPagingItemReader    |               JdbcCursorItemReader <br/> HibernateCurosrItemReader               |         JpaCursorItemReader         |
|:--------------:|:-------------------------------------------------:|:--------------------------------------------------------------------------------:|:-----------------------------------:|
| 쿼리 구현 방법 |          QueryMethod<br>QueryDSL<br>JPQL          |                                Native Query, HQL                                 |                JPQL                 |
|   동작 방식    |       Pagination<br>Limit Offset 구문 사용        |                                    Cursor방식                                    | 애플리케이션에서<br>직접 Cursor처리 |
|      성능      | 조회할 데이터가 많다면<br>뒷 Page로 갈수록 느려짐 | Cursor 기반이므로<br>Fetch size와 DB설정만 제대로 세팅하면 조회 속도가 매우 빠름 |    성능은 매우 우수하나 OOM유발     |
|                |                                                   |                                                                                  |                                     |
개선

|                |                  QueryDslZeroOffsetItemReader                  |                            ExposedCursorItemReader                            |
|:--------------:|:--------------------------------------------------------------:|:-----------------------------------------------------------------------------:|
| 쿼리 구현 방법 |                            QueryDsl                            |                                Kotlin Exposed                                 |
|   동작 방식    |  Offset을 항상 0으로 유지<br>PK를 where 조건에 추가하는 방식   |                      JdbcCursorItemReader와 동일한 방식                       |
|      성능      | 첫 Page를 읽었을 때와 동일하게<br>항상 일관된 조회 성능을 가짐 | Cursor 기반으로 많은 양의 데이터를<br>빠르게 가져오며 일관된 조회 성능을 가짐 |
# 데이터 Aggregation 처리

일차적으로 생각할때 개발자는
- `통계를 개발한다 -> Batch 로 개발한다 -> GroupBy & Sum으로 계산한다`
의 플로우를 탄다.
- [!] 하지만, 데이터가 많아지고 쿼리가 복잡해져도 문제가 없을까?
```SQL
select
sum(o.amount),
count(1),
p.price,
p.product_id,
u.age
from order o
    inner join price p
    on o.price_id = p.id
    inner join user u
    on o.user_id = u.id
where o.order_date = '2021-01-01'
and u.is_active = true
group by p.product_id, u.age
order by p.registered_at asc, u.age asc
limit 1000, 0
```
데이터 개수가 수천만개 이상으로 매우 많은 상황에서도 과연 이 쿼리는 문제가 없을까?
- 위 배치는 합산, Count연산 자체를 쿼리로 구하는 매우 쿼리에 의존적인 모습을 보여주고 있다.

> [!warning] Join+GroupBy+Sum 쿼리를 사용하면
> - 연산 과정이 쿼리에 의존적이다: Database 부하가 증가한다.
> - 데이터 누적
> 	  - 데이터 중복도(카디널리티) 변경
> 	  - 쿼리 실행 계획의 변경
> 	  - [u] 쿼리 튜닝 난이도 상승
> - 쿼리 튜닝을 위한 과도한 인덱스 추가
> 	  - [d] insert, update 성능 저하
> 	  - 저장 용량 차지

- [!] 쿼리 자체가 매우 느리기 때문에, 앞서 개선한 ItemReader가 무용지물이 되어버린다.

## 복잡한 쿼리에서 단순한 쿼리로

```SQL
--  변경 후
select
-- sum(o.amount),
-- count(1),
p.price,
p.product_id,
u.age
from order o
    inner join price p
    on o.price_id = p.id
    inner join user u
    on o.user_id = u.id
where o.order_date = '2021-01-01'
and u.is_active = true
-- group by p.product_id, u.age
-- order by p.registered_at asc, u.age asc
-- limit 1000, 0
```

직접 aggregation이 가능할까?

1. 개별 데이터는 필요 없고 Aggregation한 결과를 얻어야 한다.
	- 데이터를 가져올 때부터 Aggregation되어 있어야 처리와 저장이 쉽다.
2. 개별 데이터를 가져와 합산하려고 해도, 합산을 위한 충분한 공간과 성능이 확보되어야 한다.
	- 개별 데이터를 가져왔다고 해도, 합산을 하기 위해서는 합산 결과를 중간에 저장하기 위한 공간이 확보되어야 한다.
	- 중간 결과를 저장할 수 있는 공간을 확보했다고 하더라도, MySQL의 `GroupBy+SUM` 쿼리보다 빠르다고 장담할 수 없다.

### 동작 방식
![레디스를 이용한 아키텍처](https://tech.kakaopay.com/_astro/aggregation_new_archi.51ef254e_2gElJC.png)
1. 1000만개의 데이터를 1000개씩 나누어 만개의 chunk로 처리
2. chunk단위로 반복해서 Redis에 SUM연산 요청
3. 결국에는 50만개의 SUM데이터가 Redis에 들어있음
4. 50만개의 데이터를 최종 데이터 저장소에 저장

#### 왜 Redis일까?
1. O(1) 연산 명령어 hincrby, hincrbyfloat지원
	- 레디스는 대부분 명령어 성능이 O(1), O(n)보장되어 있다. <u>공식 문서에도 모든 명령어에 빅오 표기가 되어있다.</u>
2. 50만개는 쉽게 저장하는 넉넉한 메모리
	- 보통 Redis를 구축할 때 메모리를 최소 수십 기가에서 수백 기가바이트까지도 구축하기 때문에 수 십만 개의 인스턴스 정도는 가뿐하게 저장한다.
3. In-Memory DB로 빠르게 저장하고 영구 저장 필요 없음
	- In-Memory DB의 특성상 결과물이 디스크가 아닌 메모리에 저장돼서 연산이 매우 빠르다.
	- 최종 데이터 저장소에 저장될 때 까지만 유지하면 되므로, 영구 저장할 필요도 없다.

## Redis호출 횟수 줄이기
Redis연산 자체는 O(1)로 오래걸리지 않는다. 그러나, Redis까지 요청을 보내고 응답을 받는 networking에 드는 시간이 너무 오래걸린다.
한번 요청에 드는 시간을 1ms라고 가정하더라도, 1000만번 요청하면 약 3시간이 소요된다.

이러한 문제를 해결하기 위해 Redis Pipleline을 사용

---
[[if kakao 2022] Batch Performance를 고려한 최선의 Reader](https://tech.kakaopay.com/post/ifkakao2022-batch-performance-read/)
[\[if kakao 2022\] Batch Performance를 고려한 최선의 Aggregation](https://tech.kakaopay.com/post/ifkakao2022-batch-performance-aggregation/)