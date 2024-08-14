- 초기화
- 모델링
- 모니터링
---
# 모델링
- NoSQL 등장 배경 (2009 ~)
	- 유연한 스키마 / 분산환경
	- modernize / decupling
- RDBMS vs NoSQL 
	- SecondaryIndexes / ACID / ..
	- Flexiblilty /  Scalibility , Performance / 무중단~
	각각 장단이 있음

# DocumetDB
Document 모델을 기반으로 하는 Database이다.
- [c] NoSQL이라고 하면 `Schema free`라고 생각하기 쉬운데 이건 착각일 수 있다.
	- mysql 에서는 디자인을 하는데, NoSQfL은 Storage로 사용하려고하는데 이건 절대 안된다.

Document는 일종의 JSON. DDB나 MongoDB는[[DocumentDB AWS IMD 정리본]] 이를 `Binary 형태`로 바꿈 (text형태와 다른 장단이 있음)
- 다양한 타입 표현 가능
- 효율적

## 모델링이 필요하다.
1. Work load Define
	- 어떤 Operation이 일어나고, 이게 얼마나 보관하고, 저장하고, 어떤 빈도로 읽어올것인가
	  (이 데이터를 어떻게 만들고, 엑세스할것인가.)
	- access pattern을 정의해야한다.
	
	> 어떤 양식이 있따는 뜻이 아니고, 어떤식으로든 적어보면 된다.
	> 그러면 스펙을 어느정도로 할지 구체화됨
	> *예시*
	> - CRUD/ Frequncy / TYPE

2. Read & Write Queries
- DDB도 RDB와 동일시 실행계획같은것들을 살펴봐야한다.

# Identify RelaitonShip
noSQL이 관계가 존재하지 않는다는 착각을 하기 쉬운데 존재한다.
어떤식으로 표현하느냐가 달라지는것
- `Referenced` vs `Embed`
	그 안에 들어갈것인가, 아니면 key만 들어갈것인가
장단이 존재한다.

**Advantages**
- 내 데이터가 어떻게 acces되늦지 살펴봐야함
> 디테일한 예시 추가 필요할듯

## Many to Many는 어떻게 표현할것인가
DDB는 cross-table이 없다. id를 참조
혹은 업데이트 불필요시 그냥 넣던지..

# Design Patterns
1. Attribute pattern
	메타데이터를 표현할때 적합 
	- 이전에 속성 표현한것과 동일
```json
"attributes" : [
  {"key": "size", "value": "<string>"},
  {"key": "weight", "value": "<int>"},
  // .
  // .
  // 유연하게 늘어날 수 있다.
]	
```


2. Bucket pattern
	- 시계열 데이터 에서 많이 사용
	- 어떤건 insert, 어떤건 update인데 이건 어떻게 되는걸까
	- 거기에 따라서 장단이 존재한다. 또한 Document 에 대한 용량제한 (16) 도 존재함
	- 이 안에 몇개만 넣겠다 이런 조건이 무조건 있어야함
	- 하나의 Document

3. pre-compute pattern
	- value 밖에 추가해놓고 하나 할때마다 함께 계산하는 모델인듯??


> Document DB는 
> 스키마 버저닝을 할 수 있음. version -> 별 Key


4. Subset Pattern
	데이터를 어떻게 쪼갤것인가. 전체 데이터~


> [!tip] Document DB에서 Aggregation Pipeline
> 리눅스에서 pipline과 비슷하게, 하나하나 operator들의 function들을 따라서 쿼리가 전송됨

- mongoDB operator가 지원이 되지 않는것들 있기 때문에 개발자 가이드를 보아야 함 (Aggretateion pipeline처럼)
	- https://docs.aws.amazon.com/ko_kr/documentdb/latest/developerguide/mongo-apis.html


- 결국에는 schmealess + deployeement 할때 유리 (column하나 추가 할때 난리난리 / flexable)
- query pattern보다 api 패턴에 유리 

- `Ad Hoc Queries`
	- Document DB는 지원하기 때문에 use-case가 많음


> [!question] transaction 은 어떻게 지원하는가?
> mongoDB 4.0버전부터 transaction지원을 해준다고 생각하면됨
> - MVCC에 대한것도 있찌만 그래서 Isolation은 어떻게 지원해주는걸까?

- Dcoupled compute and storage
	- 스토리지와 컴퓨팅을 별도로 스케일 업다운을 할수있기 때문에 큰 장점이 있다!

Document DB는 Aurora Storage Engine을 사용함 MMAP은 LSM을 사용하고 WT는 B-Tree를 사용함.
- 쿼리에 따라 어떤게 빠른지가 다름


---

ㅇㅎ님 정리

## 1. 모델링

1. Nosql도 모델링이 필요함
    1. application requirements 를 먼저 파악 → db spec, relationship identify
        
    2. relationship
        
        1. referenced(linked) vs embeded
            
            1. access pattern에 따라 적절한 형태 사용
                
            2. referenced
                
                1. 1 : n object 분리하여 저장
                    
            3. embeded
                
                1. 1 : n 동일 object에 저장
                    
    3. Design Pattern
        
        1. 물리적 설계. (Access Pattern이 선행돼야 함)
            
        2. 대표적인 Patterns
            
            1. Attribute Pattern
                
                1. Metadata 등을 표현하기 좋음
                    
                2. 속성을 추가/삭제하기 편리함
                    
            2. Bucket Pattern
                
                1. 시계열 데이터를 로그성으로 모으는 1:n 관계에서 주로 사용
                    
                2. bucket 사이즈를 제한해야 함.
                    
            3. Pre-compution Pattern
                
                1. upsert할 때 document에 특정 aggregation 필드를 추가할 때 사용
                    
            4. Subset Pattern
                
                1. 너무 커진 document는 쪼개는 패턴  
                      
                    
2. DB단에 저장할 때 binary json 형태로 저장
    

## 2. Query

1. aggregation pipeline
    
    1. DocumentDB의 주요 특징
        
    2. 쿼리 결과를 다음 쿼리의 input으로 활용하여 여러 개의 쿼리를 단일 쿼리로 사용하는 기능
        

## 3. nosql 특징

1. 초기에는 ACID, Transaction을 지원하지 않았지만 최근에는 대부분 nosql에서 지원함
    
    1. mongodb 4.0 이상부터 지원
        
2. Decoupled Architecture
    
    1. computing layer(api, query processor, caching), storage layer(loging, storage)를 분리한 아키텍처
        
    2. 각각의 layer를 스케일링하기 용이 (기존 RDBMS 방식의 단점을 보완)
        
    3. 서비스 특성에 따라 Coupled Architecture 혹은 Decoupled Architecture 중 유리한 형태를 선택하면 됨
        
    4. DocumentDB도 샤딩을 제공하긴 하지만 write연산이 과도하게 많을 때 사용
        
3. 일반적으로 하나의 노드는 write, 나머지는 read용
    
    1. 멀티 write를 하려면 샤딩이나 elastic cluster 사용