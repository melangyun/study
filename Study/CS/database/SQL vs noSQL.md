![데이터 베이스 종류](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkKtTE%2FbtrmgFa2t9M%2FXBfLBPrksvVoRFbqVJr4EK%2Fimg.png)


[NoSQL vs RDB](https://siyoon210.tistory.com/130)

>[!tip] 왠만하면 SQL이 좋다.
>noSQL은 특별한 이슈에 대응하기 좋은 DB이다.
>대부분의 경우 그러한 이슈가 없다.
>(데이터의 정합도가 중요하다면 관계형 DB추천!)

# 장점 vs 단점

## 장점
- SQL
	- 명확하게 정의 된 스키마, 데이터 무결성 보장
	- 관계는 각 데이터를 중복없이 한번만 저장
- NoSQL
	- 유연한 스키마
	- 즉, 언제든지 저장된 데이터를 조정하고 새로운 "필드"를 추가 할 수 있습니다.
	- 데이터는 애플리케이션이 필요로 하는 형식으로 저장.
	- <u>수직 및 수평 확장이 가능</u>하므로 데이터베이스가 애플리케이션에서 발생시키는 모든 읽기 / 쓰기 요청을 처리 할 수 있다
## 단점
수평적 확장 -> NoSQL이 유리
- SQL
	- 상대적으로 덜 유연. 데이터 스키마는 사전에 계획되어야 한다.
	  (나중에 수정하기가 번거롭거나, 불가능하다)
	- 관계때문에 join문이 많은 복잡한 쿼리가 만들어질 수 있다.
	- 수평적 확장이 어렵고, 대체로 수직적 확장만 가능하다.
	  즉 어떤 시점에서 (처리 할 수 있는 처리량과 관련하여) 성장 한계에 직면하게 된다.
- NoSQL
	- 데이터 구조가 명확하지 않아질 수 있다.
	-  중복된 데이터에 대하여 레코드가 변경된 경우 업데이트를 여러번 해야 한다.

.

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZVuHZ2Fjkl4?si=mU_sl1pIgDBJImFe&amp;controls=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Q_9cFgzZr8Q?si=f-a1M7WMMj_PiVXv&amp;controls=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

> [!tip] NoSQL (Not only SQL || Not SQL)
> 그러나, 한가지 데이터베이스만을 의미하는것이 아니다!
> 단순히, SQL을 사용하지 않는 모든 DB를 의미하는것 이기도하다.

![nosql 종류](https://media.geeksforgeeks.org/wp-content/uploads/20220405112418/NoSQLDatabases.jpg)



> [!warning] SQL DB는 무엇이 있을까?
> Mysql, Oracle, PostgreSQL, SQLite..
> > 결국 SQL이라는 점은 동일하다

# NoSQL의 종류

## 1. Document
데이터를 json document형태로 저장한다.
따라서 무슨 형태든 저장 가능하며, 데이터가 같은 모양일 필요가 없다.
> 정규화와 데이터 중복제거를 하지 않는다.

- mongoDB

## 2. Key-value

- cassandra db
	column wide database 유형이기도 하다.
	읽고 쓰는 속도가 매우 빠르다. -> 애플, 넷플릭스, 우버가 사용
	혹은 검색엔진처럼 많은 양의 데이터를 빠르게 읽어야 할때 적합하다.
- Amazon [[DynamoDB]]
	Serverless, 분산된 key-value DB
	무려 초당 24,000개의 읽기를 지원함
	엄청 빠르게 읽고, 써야할때 필요함

하지만 sql처럼 검색은 할 수 없음

## 3. GraphDB
관계와 방향을 모두 표현할수 있다.
column이나, Document가 필요 없지만, 각 노드 사이의 관계를 알아야 할 때
ex) 소셜 네트워크를 만든다면 필요할수 있음
-> Graph query language를 사용해야 한다.

- noe4j

---
연관링크
[[nosql]]

