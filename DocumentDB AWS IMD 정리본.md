# NoSQL 등장배경
2009년 이후 `빅데이터` 가 등장하며 다양한 규모의 데이터를 처리하기 위해 더 유연하고 확정성 높은 데이터 베이스가 필요해졌다. 전통적인 RDBMS보다 더 유연하고 확장성이 높은 데이터베이스의 필요성에 의해 여러 NoSQL이 등장하였다.

RDBMS와 NoSQL은 각각의 철학과 설계 목표에 따라 차이가 있기때문에, 단순히 RDBMS의 동일선상에서 NoSQL을 사용하는것이 아니라, 각각의 특성과 장단을 이해하고 이를 사용하는것이 중요하다.

> [!summary] 보편적으로 생각하는 NoSQL / RDBMS의 장단
> - **Secondary Indexes**
> 	- RDBMS는 강력한 SecondrayIndex를  지원
> 	- NoSQL은 RDBMS만큼 성능이 나오지 않거나 오히려 저하될 수 있고, 분산된 환경에서 인덱스 관리가 복잡해 질 수 있음
> - **ACID**
> 	- RDBMS는 전통적으로 ACID준수
> 	- 그러나 NoSQL은 CAP에 기반하여 ACID를 모두 준수하지 않을 수 있음 (최종적 일관성 모델)
> - **Flexibility**
> 	- RDBMS는 엄격한 스키마 요구. 이로 인해 모델 변경-확장시 제약 존재
> 	- NoSql은 보통 유연한 스키마 혹은 schemaless 
> - **Scalability** / **Performance**
> 	- NoSQL은 분산환경의 수평확장에 장점. (고가용성). 
> 	- 무중단 운영 (Zero-Downtime)
> 	  
> 등등등...

# DocumentDB
AWS에서 제공하는 NoSQL 데이터베이스 서비스. MongoDB와 호환되는 API를 제공하며, MongoDB에서 사용되는 쿼리 언어, 데이터 모델, 드라이버를 사용할 수 있다.
> 그러나, 분명 여러 차이가 존재하며 완전히 호환되지 않는다는 부분도 유의.
> \[[MongoDB_Comparing Amazon DocumentDB and MongoDB](https://www.mongodb.com/resources/compare/documentdb-vs-mongodb)\]
## MongoDB vs DocumentDB

