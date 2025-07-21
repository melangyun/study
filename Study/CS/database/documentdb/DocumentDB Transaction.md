[AWS DocumentDB Transaction](https://docs.aws.amazon.com/ko_kr/documentdb/latest/developerguide/transactions.html#transactions-errors)
- Amazon DocumentDB 4.0 엔진 사용
- MongoDB 4.0 이상과 호환되는 드라이버 사용하고 있어야함

# 제한
## 2. `cursor`를 지원하지 않음
```js
// mongodb에서는 DB 질의 결과를 순차적으로 처리하기 위한 포인터의 개념으로 커서를 지원

const cursor = db.collection("users").find({age: {$gt: 30}})

while(await cursor.hasNext()){
  const user = await cursor.next()
  
}
```
트랜잭션이 열려있는 상태에서 커서를 열고, 순차적으로 next를 호출하는 동작이 되지 않는다.
- MongoDB는 4.0버전부터 multi-document transaction을 지원하고, 그 안에서 커서도 함께 사용할 수 있다.
	- 하지만 기본적으로 60초 내에 commit해야함.

## 3. 트랜잭션에서 새 컬렉션을 생성할 수 없으며, 존재하지 않는 컬랙션에 대해 쿼리 / 업데이트를 할 수 없음
```js
const session = client.startSession();
session.startTransaction();

await db.collection("new_collection").insertOne({ name: "test" }, { session });
// mongoDB의 경우 컬렉션 자동 생성 허용 but DocumentDB는 에러 발생
await session.commitTransaction();
```

## 4. 문서 수준 쓰기 잠금에는 사용자가 구성할 수 없는 1분의 제한 시간이 적용됨
Document 
