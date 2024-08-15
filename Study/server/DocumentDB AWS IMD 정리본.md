# NoSQL 등장배경
2009년 이후 `빅데이터` 가 등장하며 다양한 규모의 데이터를 처리하기 위해 더 유연하고 확정성 높은 데이터 베이스가 필요해졌다. 전통적인 RDBMS보다 더 유연하고 확장성이 높은 데이터베이스의 필요성에 의해 여러 NoSQL이 등장하였다.

RDBMS와 NoSQL은 각각의 철학과 설계 목표에 따라 차이가 있기때문에, 단순히 RDBMS의 동일선상에서 NoSQL을 사용하는것이 아니라, 각각의 특성과 장단을 이해하고 이를 사용하는것이 중요하다.

# DocumentDB

AWS에서 제공하는 Document모델 기반 NoSQL 데이터베이스 서비스. MongoDB와 호환되는 API를 제공하며, MongoDB에서 사용되는 쿼리 언어, 데이터 모델, 드라이버를 사용할 수 있다.

> 그러나, 분명 여러 차이가 존재하며 완전히 호환되지 않는다는 부분도 유의해야한다.
> - [아마존 DocumentDB와 MongoDB](https://docs.aws.amazon.com/ko_kr/documentdb/latest/developerguide/functional-differences.html)
> - [aws_documentDB에서 지원되는 MongoDBAPIs](https://docs.aws.amazon.com/ko_kr/documentdb/latest/developerguide/mongo-apis.html)

- [!] NoSQL이라라고 하면 `Schema-less`라고 생각하고 RDB에서 하던 설계를 생략해버리기 쉬운데, 이렇게 사용해서는 안된다.
	- 잘못된 스키마 설계는 ==성능과 비용 측면==에서 큰 영향을 미칠 수 있기때문

**Document**
Document는 일종의 JSON이다. DocumentDB나, MongoDB에서는 이를 Binary 형식의`BSON(Binary JSON)`으로 변경하여 저장한다.
- 1Document당 `16MB`로 제한이 있다.
- [!] Write IO는 `4kb` 단위, Read IO는 `8kb`단위로 계산된다. 따라서 문서당 크기를 8kb제한하는것이 이상적이다.

**Collections**
Collections는 문서의 그룹이며, 유사한 내용을 가진 문서를 저장한다. Document DB는 유연한 스키마가 제공되기 때문에, 컬렉션의 모든 문서에 동일한 필드가 필요한것은 아니다. 
일부 Document DB는 스키마 유효성을 제공하기 때문에, 스키마를 선택적으로 잠글 수 있다.

- RDB: 복잡한 트랜잭션이 필요하고, 데이터 관계가 명확하게 정의된 경우(ex: 금융 시스템, 주문관리 시스템)
- DocumentDB: 비정형 데이터나 빈번한 데이터 구조 변경이 발생하는 경우(Ex: 콘텐츠 관리, IoT, Catalogs)

# 스키마 모델링 기법
그렇다면 스키마 모델링을 어떻게 할것인가?
> [Data modeling with Amazon DocumentDB (with MongoDB compatibility) - AWS Online Tech Talks](https://www.youtube.com/watch?v=mZVn1ZS6jCM)

> [!warning] Most common anti-patterns
> - 배열 내 너무 많은 요소가 포함된 경우
> 	- ==모든 배열은 제한없이 커지면 안된다.==
> -  중복되거나 사용되지 않는 인덱스
> - 너무 큰 문서(Large Documents)
>
>슬로우 쿼리, 높거나 예상치 못한 IOPS, 비효울적인 캐시 사용이 일어날 수 있음
>- **단기 해결책**: 인스턴스 크기 증가, 인스턴스 추가(수평 확장)
>- **장기 해결책**: 스키마 재설계, access Pattern 검토, 인덱싱 전략 검토

1. Work Load Define
2. Read & Write Queries

 어떤 Operation 이 일어나고, 얼마나 보관되고, 어떤 빈도로 읽어올것인가. access pattern 정의가 필요하다.
> 어떤 양식이 있지는 않고, 어떤식으로든 정리하고 적어보면 된다. 그러면 스펙을 어느정도로 할지 구체화됨

 - 또, DocumentDB도 RDB와 동일히 실행 계획도 살펴봐야한다

## Identify RelationShip
- [MongoDB_Embeded_vs_Embed](https://www.mongodb.com/docs/manual/data-modeling/concepts/embedding-vs-references/)
DocumentDB에서도 관계가 존재한다. (RDB와는 표현방식은 다르다) 
- `References` vs `Embed`
각각의 장단을 파악하고 상황에 맞는 모델을 선택해야한다

### Embed
![임베디드 데이터 모델](https://www.mongodb.com/ko-kr/docs/manual/images/data-model-denormalized.bakedsvg.svg)
자주 액세스 하는 데이터가 여러 컬렉션에 중복되어 나타난다면, 비정규화되는 경우가 많다.

**UseCases**
- 엔티티간 포함관계가 있음
- 엔티티가 1:N 관계에 있음
읽기 작업 성능이 향상하며, 단일 작업에서 관련 데이터를 검색할 수 있다.

### References
![References](https://www.mongodb.com/docs/manual/images/data-model-normalized.bakedsvg.svg)
여러 컬렉션으로 나뉘고, 중복되지 않은 정규화된 데이터 모델

**Use Cases**
- Embed 시 데이터가 중복되지만, 중복으로 인한 영향을 능가할 만큼 읽기 성능이 충분하지 않을경우
	- ex) 내장된 데이터가 자주 변경되는 경우
- 복잡한 다대다 관계나, 대규모 계층적 데이터 세트를 표현해야 할 경우

- [?] Many to Many 의 관계는 어떻게 표현할것인가?
```js
// 서로의 id 참조
const StudentSchema = new Schema({
  name: String,
  courses: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Course' }]
});

const CourseSchema = new Schema({
  name: String,
  students: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Student' }]
});
```
혹은 일부 비정규화하여 표현: [_Many-to-Many Relationships in MongoDB for Enhanced Database Management](https://medium.com/mongodb-tutorial/solving-the-many-to-many-relationship-challenge-in-mongodb-125b0421b6f0)

# Design Patterns

## 1. Attribute Pattern
[mongoDB_Attribute](https://www.mongodb.com/blog/post/building-with-patterns-the-attribute-pattern)
메타데이터를 표현할 때 적합하다.
```js
// Movie Collection
{
    title: "Star Wars",
    director: "George Lucas",
    ...
    release_US: ISODate("1977-05-20T01:00:00+01:00"),
    release_France: ISODate("1977-10-19T01:00:00+01:00"),
    release_Italy: ISODate("1977-10-20T01:00:00+01:00"),
    release_UK: ISODate("1977-12-27T01:00:00+01:00"),
    ...
}
```
Attributes Pattern을 이용하여, 정보를 하위 subset으로 이동.
필드를 Key-value 짝으로 나누어 서브 도큐먼트에 저장
```js
{
    title: "Star Wars",
    director: "George Lucas",
    …
    releases: [
        {
        location: "USA",
        date: ISODate("1977-05-20T01:00:00+01:00")
        },
        {
        location: "France",
        date: ISODate("1977-10-19T01:00:00+01:00")
        },
        {
        location: "Italy",
        date: ISODate("1977-10-20T01:00:00+01:00")
        },
        {
        location: "UK",
        date: ISODate("1977-12-27T01:00:00+01:00")
        },
        … 
    ],
    … 
}
```
## 2. Pre-computed Pattern
[MongoDB_The Computed Pattern](https://www.mongodb.com/blog/post/building-with-patterns-the-computed-pattern)
데이터에 대한 계산이 많을때. 같은 데이터에 자주 접근해서 같은 결과를 계산해야 할 때.
- 계산된 데이터를 도큐먼트에 저장하고, 다음번에 데이터가 필요할 때 미리 계산된 데이터를 사용한다.
![computed_pattern](https://webassets.mongodb.com/_com_assets/cms/cpucomputed-fbcpkmvbsy.png)

## 3. Bucket Pattern
[MongoDB_Bucket](https://www.mongodb.com/blog/post/building-with-patterns-the-bucket-pattern)
Document가 너무 많아졌을 경우. 임베딩하기 어려운 1:N 관계에서 사용
시계열 데이터에서 많이 사용한다.
- 그룹화할 적정량의 데이터를 지정하고
- 메인 Document에 array를 만들어 저장한다.
```js
// 만일 매 분마다 온도를 측정하는 데이터가 쌓이는 경우
{
   sensor_id: 12345,
   timestamp: ISODate("2019-01-31T10:00:00.000Z"),
   temperature: 40
}

{
   sensor_id: 12345,
   timestamp: ISODate("2019-01-31T10:01:00.000Z"),
   temperature: 40
}

{
   sensor_id: 12345,
   timestamp: ISODate("2019-01-31T10:02:00.000Z"),
   temperature: 41
}
```
Bucket Pattern 적용 후
- 1시간 버킷으로 '버킷화'함.
- 데이터 추가시 `transaction_count`와 `sum_temperature` 함께 업데이트됨
```js
{
    sensor_id: 12345,
    start_date: ISODate("2019-01-31T10:00:00.000Z"),
    end_date: ISODate("2019-01-31T10:59:59.000Z"),
    measurements: [
       {
       timestamp: ISODate("2019-01-31T10:00:00.000Z"),
       temperature: 40
       },
       {
       timestamp: ISODate("2019-01-31T10:01:00.000Z"),
       temperature: 40
       },
       … 
       {
       timestamp: ISODate("2019-01-31T10:42:00.000Z"),
       temperature: 42
       }
    ],
   transaction_count: 42,
   sum_temperature: 2413
} 
```
## 3. Subset Pattern
[MongoDB_SubsetPattern](https://www.mongodb.com/blog/post/building-with-patterns-the-subset-pattern)
작업 데이터가 너무 커서 메모리에 캐시를 유지하기 어려울때.
혹은 Document의 큰 부분이 자주 사용되지 않는 경우
![subset1](https://webassets.mongodb.com/_com_assets/cms/docsubset2-ncq6t9lt01.png)
제품에는 최근 10개 정도의 리뷰가 필요할 가능성이 크다. 모든 리뷰를 Product 하위에 넣기에는 working set이 너무 커지게 된다.

따라서, 두개의 컬랙션으로 나눠볼 수 있을것이다.

## 4. Schema Versioning Pattern
동일한 컬렉션에 여러 Document 모델이 존재할때. 애플리케이션을 가동 중지할 수 없거나, 문서를 새 버전으로 업데이트 하고싶지 않을때, 마이그레이션 시기 조정이 필요할때 사용
```json
{
    "_id": "<ObjectId>",
    "name": "Anakin Skywalker",
    "home": "503-555-0000",
    "work": "503-555-0010"
}
```
- schema_version 필드 추가.
- 애플리케이션 버전 별 처리 및 마이그레이션 전략 수립
```js
{
    "_id": "<ObjectId>",
    "schema_version": "2",
    "name": "Anakin Skywalker (Retired)",
    "contact_method": [
        { "work": "503-555-0210" },
        { "mobile": "503-555-0220" },
        { "twitter": "@anakinskywalker" },
        { "skype": "AlwaysWithYou" }
    ]
}
```

# Query
- DocumentDB는 MongoDB에서 사용하는 쿼리 언어를 지원하기 때문에 에드훅 쿼리에 대한 use-case가 많다.

- [?] 복잡한 조인문을 DocumentDB에서는 어떻게 조회해 올 수 있을까?
	- [p] Aggregation Pipeline을 사용하면 된다!

```js
db.collection.aggregate([
   { $match: { age: { $gte: 18 } } },  // 나이가 18세 이상인 문서 필터링
   { $group: { _id: "$city", averageAge: { $avg: "$age" } } },  // 도시별로 그룹화하고 평균 나이 계산
   { $sort: { averageAge: -1 } },  // 평균 나이를 기준으로 내림차순 정렬
   { $limit: 5 }  // 상위 5개 도시만 반환
])
```
---
### MongoDB와 DocumentDB는 유사하지만 스토리지 엔진이 다르기때문에 애플리케이션의 특징과 어떤 쿼리를 많이 사용할지에 따라 유리한 DB가 달라질 수 있다.

DocumentDB는 Aurora Storage Engine을 사용한다. 분산 스토리지 아키텍처를 사용하며, HA와 복원력을 제공하는데 최적화 되어있다. AZ에 자동 복제하므로, 읽기 성능과 가용성이 뛰어남

MongoDB는 WiredTriger 스토리지 엔진을 사용하며, B-Tree 기반의 인덱싱과 데이터 저장방식을 사용. DocumentDB는 읽기성능에 특히 더 강점을 가지며, 분산 스토리지 아키텍처 덕분에 여러 노드에서 데이터를 동시에 읽어오는 작업이 효율적이다.
- 쓰기작업은 하나의 리더노드에서 처리되며, 이를 다른 가용영역으로 복제하는 방식으로 작동
따라서 쓰기 작업이 많은 경우 DocumentDB가 MongoDB보다 성능이 떨어질 수 있다. 
MongoDB의 WiredTiger는 쓰기 성능과 동시성 처리에 강점을 가지고 있다. 빈번한 업데이트, 삽입작업 시 더 유리할 수 있음.


[Introduction to data modeling with Amazon DocumentDB (with MongoDB compatibility) for relational database users](https://aws.amazon.com/ko/blogs/database/introduction-to-data-modeling-with-amazon-documentdb-with-mongodb-compatibility-for-relational-database-users/)