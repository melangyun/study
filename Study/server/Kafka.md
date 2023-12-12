직카프카는 [[PUB-SUB]] 을 따르고 있다.

![카프카 브로커](https://blog.kakaocdn.net/dn/mrQ5A/btqC2uxbCkj/dbs2YwdDz86LpAoJmBNa5K/img.png)

# **Kafka 만들게 된 이유**

스트림(시간이 흐르면서 사용할 수 있게 되는 데이터 요소)으로 데이터를 처리하는 방법에 중점을 둔 시스템을 개발하기 위해서 개발되었다.

Kafka는 실시간으로 데이터 스트림을 수집하여 처리합니다
Kafka 공식 홈페이지 첫 화면에는 Kafka를 '오픈소스 분산 이벤트 스트리밍 플랫폼'으로 표현하고 있다.
> 스트리밍 플랫폼(Streaming Platform)은 데이터 스트림을 읽고 쓰고 저장하고 처리하는 역할을 가진 시스템을 의미한다.

kafka는 메시지 스트림을 쓰고 읽게 해주는 메시징 시스템(ActiveMQ, RabbitMQ)과 같다.

# Kafka특징

## 클러스터로 실행된다.

서로 다른 애플리케이션을 수동으로 연결하는 많은 개별적인 메시징 브로커들 대신 회사의 모든 데이터 스트림 처리를 위해서 탄력적으로 확장할 수 있는 하나의 ‘중심 플랫폼’ 역할을 한다.

![카프카 클러스터](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAQBw8%2FbtriFjnh9Zi%2FNkHEE6lm7ePptlKhs8ucrk%2Fimg.png)


## 원하는 기간동안 데이터를 저장하기 위해 만들어진 스토리지 시스템이다.

신뢰성 있는 데이터의 전달을 보장하고 있다. Kafka를 서로 다른 시스템의 연결 계층으로 사용할 수 있다. Kafka 의 데이터는 복제되고, 영구적이며, 원하는 만큼 보존 가능하다.

## 스트림 프로세싱(Stream Proccessing) 능력이 있다.

> 메시징 시스템은 단순히 메시지 전달에만 초점을 두고있다.

하지만 Kafka는 훨씬 더 적은 코드로 스트림으로부터 파생된 다른 스트림과 데이터 세트를 산출해 낼 수 있는 스트림 프로세싱 능력이 있다.

> [!info] 스트림 프로세싱 능력이란?
> ![스트림 프로세싱](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcuiTuH%2FbtriCvVWKx0%2FcYNH9H48QiLjGy8B1tDQf1%2Fimg.png)
>**연속적으로 들어오는 데이터에 대한 여러 작업을 처리하는 것을 의미**
> - 집계(예: 합계, 평균, 표준 편차와 같은 계산)  
> - 분석(예: 데이터의 패턴을 기반으로 미래 이벤트 예측)  
> - 변환(예: 숫자를 날짜 형식으로 변경)이 포함됩니다. )  
> - 강화(예: 데이터 포인트를 다른 데이터 소스와 결합하여 더 많은 컨텍스트 및 의미 생성)  
> - 수집(예: 데이터를 데이터베이스에 삽입)
>   > **Stream Processing**
> Stream Processing 은 Hadoop으로 했던 Batch Processing 의 상위 개념이다.
> Hadoop의 실시간 버전으로 카프카가 설계되었다.


# 메시지 발행/ 구독

## 메시지
카프카 메시지의 구조는 다음과 같다.
- 토픽 (Topic)
- 토픽 중 특정 파티션 위치 (Partition)
- 메시지 생성 시간 (Timestamp)
- 메시지 키 (Key)
- 메시지 값 (Value)

## 프로듀서 구조와 메시지 전달 과정

 프로듀서는 다음 4가지 과정을 통해 메시지를 브로커로 전달한다.
 이 과정은 **브로커에 메시지를 전송할 수 있도록 변환하거나, 필요한 값을 지정해주는 과정이다.**
![메시지가 브로커로 전달되는 과정](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXvurH%2FbtqCJlT9MAh%2FzZK1T4QjFh3aTqibOMXRuk%2Fimg.png)
1. 직렬화 (Serializer)
	요청받은 메시지를 직렬화 한다. 직렬화(Serialization)는 Serializer가 지정된 설정을 통해 처리하며, **메시지의 키와 값은 바이트 뭉치 형태로 변환된다**
2. 파티셔닝 (Partitioner)
	직렬화 과정을 마친 메시지는 Partitioner를 통해 **토픽의 어떤 파티션에 저장될지 결정된다.**
	Partitioner는 정의된 로직에 따라 파티셔닝을 진행하는데, 별도의 Partitioner 설정을 하지 않으면 Round Robbin 형태로 파티셔닝을 한다. (즉, 파티션들에게 골고루 전달할 수 있도록 파티셔닝을 한다.)
	> 단, 이 과정은 메시지 전달 요청에 파티션이 지정되지 않았을 경우에만 진행
3. 메시지 배치 (Record Accumulator)
4. 압축 (Compression)
	만약 메시지 압축이 설정되었다면, 설정된 포맷에 맞춰 메시지를 압축
5. 전달 (Sender)
	 파티셔닝과 압축을 마친 후, 프로듀서는 메시지를 TCP 프로토콜을 통해 브로커 리더 파티션으로 전송
	 하지만 메시지마다 매번 네트워크를 통해 전달하는 것은 비효율적이기에, 프로듀서는 지정된 만큼 메시지를 저장했다가 한 번에 브로커로 전달한다.
> 	이 과정은 프로듀서 내부의 Record Accumulator(RA)가 담당하여 처리한다. RA는 각 토픽 파티션에 대응하는 배치 큐(Batch Queue)를 구성하고 메시지들을 레코드 배치(Record Batch) 형태로 묶어 큐에 저장.

각 배치 큐에 저장된 레코드 배치들은 때가 되면 각각 브로커에 전달되며 이 과정은 Sender가 처리한다. 
Sender는 스레드 형태로 구성되며, **관리자가 설정한 특정 조건에 만족한 레코드 배치를 브로커로 전송한다.** 이때, Sender 스레드는 네트워크 비용을 줄이기 위해 **piggyback 방식**으로 조건을 만족하지 않은 다른 레코드 배치를 조건을 만족한 것과 함께 브로커로 전송한다. 


발행자가 어떤 형태로든 메시지를 구분하여 발행/구독 시스템에 전송한다
> cf) [[EDA(Event Driven Architecture)이란?#^aba780]]

발행/구독 시스템에 전송이 되면 구독자에게 특정 부류의 메시지를 구독할 수 있게 해준다.
이때, 발행되어진 <u>메시지를 저장하고 중계 역할</u>을 `브로커(broker)` 가 수행한다.

## 메시지 발행/ 구독 시스템 아키텍처

1. 발행자- 구독자 직접 연결
	![발행자-구독자 직접 연결](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmO0SG%2FbtriFh4hofk%2FFh8NZ2bvoxnKoVNq7Z0kWk%2Fimg.png)
2. 발행-구독 시스템 아키텍처
   ![발행-구독 시스템 아키텍처](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWMCW3%2FbtriB7ah0Au%2F1cZ6KhDfmdNVdkClQcxU8k%2Fimg.png)
3. 여러 종류의 발행-구독 시스템 아키텍처
	![여러종류의 발행-구독 시스템 아키텍처](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcZ4iR4%2FbtriBcQFlMO%2F2eiSYhV7tNW8jQfDYwAj91%2Fimg.png)
> [!attention] 결국 다수의 메시지 처리 시스템을 유지 및 관리해야 하는 문제가 생간다.

> [!check] 이 문제를 카프카를 이용해 해결 할 수 있다.
일반화된 유형의 메시지 데이터를 발행/구독하는 하나의 집중 처리 시스템으로 만들게 된다. 하나의 시스템으로 관리하므로 유연성과 확장성이 좋다.

# 카프카의 메세지 데이터

![카프카의 토픽과 파티션](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*dEeuSOb7Z8K7---q.png)

카프카의 메시지 데이터는 `토픽(topic)` 으로 분류된 `파티션(partition)`에 수록된다.
이때, 데이터를 <u>수록할 파티션을 결정하기 위해 일관된 해시 값으로 키를 생성</u>한다.
> 파티션 내의 한 칸은 `로그`라고 불린다.
> 메시지의 상대적인 위치를 나타내는 것이 `offset`이다.

> [!question] 왜 하나의 토픽에 여러개의 파티션이 있을까?
>  하나의 토픽에 여러개의 패티션이 있다면 *병렬 처리*를 할 수 있다.

>[!warning] 하지만 너무 많은 파티션이 있다면 좋지만은 않다.
>1. 리더-팔로워 동기비용 증가
>2. 컨슈머 그룹의 불균형한 분배
>3. Zookeeper 오버헤드
>	카프카는 Zookeeper를 이용해서 메타데이터와 브로커 간 조정을 관리하는데, 파티션 수가 많아지면 Zookeeper에 대한 부하가 증가 할 수 있다.
>4. 모니터링 및 클러스터 관리의 어려움



>[!info] kafka는 메시지 직렬화 프레임워크 Avro를 사용한다.
>>메시지는 JSON, XML 형식을 사용할 수 있다. 하지만, 타입에 대한 지원이 부족하고 스키마 버전 간의 호환성이 낮은 문제가 있다.
>
>이를 해결하기 위해 Avro 사용한다. Avro는 데이터를 직렬화하는 형식을 제공한다.
>메시지와 별도로 스키마를 유지 관리하므로 스키마가 변경되어도 애플리케이션 코드를 수정할 필요가 없다.

# 토픽과 파티션

하나의 토픽은 여러 개의 파티션으로 구성될 수 있다.

![토픽과 파티션](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fct5YvK%2FbtriB6ifCqq%2Fh4STvmsuzKHSkDaKqzfsA0%2Fimg.png)

메세지는 파티션에 추가만 해주는 형태이며, 추가되는 메시지는 각 파티션의 끝에 수록된다.
메시지 처리 순서는 토픽이 아닌 파티션별 유지, 관리된다. 파티션은 서로 다른 서버에서 분산하여 처리할 수 있다.

## Kafka 시스템의 스트림(Stream)

파티션 개수와 상관없이 <u>하나의 토픽 데이터로 간주</u> 된다. 데이터를 쓰는 Produce로부터 데이터를 읽는 Consumer로 이동되는 연속적인 데이터를 나타낸다

# Kafka의 구조

![카프카의 구조](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*Wb1KAsJRad_QEX2Z.png)

- Comsumer
	하나 이상의 Topic을 구독한다.
	메시지는 생성된 순서대로 읽으며 메시지의 **오프셋**을 유지하고 있어, 읽고있는 메시지의 위치를 알 수 있다.
	> 컨슈머가 메시지 읽기를 중단하여도, 이어서 읽을 수 있다.	

- Comsumer Group
	consumer들의 묶음이다.
	- [f] **반드시 해당 topic의 파티션은 그 consumer group과 1:n 매칭을 해야한다.**
	만약 partition의 갯수보다 Comsumer의 갯수가 많아지면 안된다(Comsumer이 놀게됨)
	> 한 토픽의 '각 파티션'은 '하나의 컨슈머'만 소비할 수 있다.
	> '각 컨슈머'가 '각 파티션'에 대응되는 것을 파티션 소유권(ownership) 이라고 한다.

> [!question] Consumer Group이 존재하는 이유가 뭘까?
> 컨슈머 그룹은 하나의 topic에 대한 책임을 갖고 있다.
> 같은 그룹 내의 컨슈머가 다운된다면, 파티션 재조정(리밸런스)를 통해 다른 컨슈머가 파티션 소비를 이어서 하게된다.
> > 위에서 설명한 `offset`의 위치를 알고 있기 때문에 문제가 생기지 않는다.

# 브로커(Broker), 클러스터(Cluster), Zookeeper


하나의 카프카 서버를 `브로커(broker)`라고 한다.
> 동일 노드 내에서 여러개의 broker 서버를 띄울 수도 있다.

>[!info] 이러한 분산 메시지 큐의 정보를 관리해 주는 역할을 하는것이 Zookeeper

`브로커(Broker)`는 `서(Producer)`로부터 `메시지(Topic)`를 수신하고 `오프셋(offset)` 을 지정한 후 <u>해당 메시지를 디스크에 저장</u>한다.
- [*] kafka의 핵심 기능 중 하나는 보존이다! 일정 기간 메시지를 보존한다.

Kafka의 클러스터는 브로커의 일부로 동작하도록 설계되어 있다.
여러개의 브로커가 하나의 클러스터에 포함될 수 있다.
기본적으로 토픽을 보존 설정한다.

# 클러스터 컨트롤러(Kluster Controller)

클러스터 컨트롤러는 같은 클러스터의 각 브로커에게 담당 파티션을 할당한다.
클러스터 컨트롤러는 브로커들이 정상적으로 동작하는지 모니터링 관리 기능을 맡고 있다.

![kafka Cluster Controller](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FctpGrZ%2FbtriAGdtOaR%2FHy6BPK2nfC6B43nEuXfYN1%2Fimg.png)

각 파티션은 클러스터의 한 브로커가 소유하며, 그 브로커를 파티션 리더l(leader)라고 한다.
같은 파티션이 여러 브로커에 지정될 수 있으며 이때는 해당 파티션이 복제된다.

파티션의 메시지는 중복으로 저장되지만
한 브로커에 장애가 생기면 다른 브로커가 소유권을 인계받아 그 파티션을 처리할 수 있다.

> [!tip] 각 파티션을 사용하는 모든 컨슈머, 프로듀서는 파티션 리더에 연결해야 한다.

# 다중 클러스터

**다중 클러스터의 장점**

1. 데이터 타입에 따라 구분하여 처리할 수 있습니다
2. 보안 요구사항을 분리해서 처리할 수 있습니다
3. 재해 복구를 대비한 다중 데이터센터를 유지할 수 있습니다

# 다중 데이터센터 아키텍처

![다중 데이터센터 아키텍처](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Frf7SJ%2FbtriGjHC0xl%2Fk3jurlzXCsE8EGrJFhkx31%2Fimg.png)

데이터센터 B의 카프카 클러스터를 -> 미러메이커 A를 이용해 -> 카프카 집중 클러스터 A에 생산할 수 있다.

데이터센터 B의 카프카 집중 클러스터 B를 -> 미러메이커 C를 이용해 -> 카프카 집중 클러스터 C에 생산할 수 있다.



# 카프카를 선택하는 이유

1. 다중 프로듀서
   여러 Producer가 많은 Topic을 사용해도, 같은 Topic을 함께 사용해도 무리 없이 많은 Producer 메시지를 처리할 수 있다. 여러 프런트엔드 시스템으로부터 데이터를 수집하고 일관성을 유지하는데 이상적이다.
2. 다중 컨슈머
   Kafka는 많은 Consumer가 상호 간섭없이 어떤 메시지 스트림을 읽을 수 있게 지원한다.<u>한 클라이언트가 특정 메시지를 소비하면 다른 클라이언트에서 그 메시지를 사용할 수 없는 큐(queue) 시스템과 다르다.</u>
   Kafka Consumer는 Consumer Group의 멤버가 되어 메시지 스트림을 공유할 수 있다(Consumer Group 이미지 참고)
3. 확장성
   Kafka는 어떤 크기의 데이터도 쉽게 처리할 수 있음 (크던, 작던)
   확장 작업은 시스템 전체 사용에 영향을 주지 않고 클러스터가 온라인 상태일 때도 수행될 수 있다. 여러 개의 브로커로 구성된 클러스터는 개별적인 브로커의 장애를 처리하면서 클라이언트에게 지속적인 서비스를 할 수 있다. 동시에 여러 브로커에 장애가 생겨도 정상적으로 처리할 수 있습니다. ‘복제 팩터’를 더 큰 값으로 지정하여 구성할 수 있다.
4. 영속성
   메시지(Topic)를 디스크에 저장함으로써 영속성을 보장한다.
   장애 발생시에도 Producer의 개입 없이 offset rewind를 통해 데이터를 다시 보내주는 것이 가능하다.
   > (데이터 정합성을 지키기 어려운 MSA 환경에서 매우 중요한 요소입니다.)

(디스크에 저장함에도 불구하고 디스크 순차 I/O 읽기와 Zero Copy 기법으로 메모리와 같이 빠른 성능을 보여주고 있습니다.)

---
[Kafka 이벤트 스트리밍 이해하기](https://wjjeong.tistory.com/56)
[Kafka 이해하기](https://medium.com/@umanking/%EC%B9%B4%ED%94%84%EC%B9%B4%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%9D%B4%EC%95%BC%EA%B8%B0-%ED%95%98%EA%B8%B0%EC%A0%84%EC%97%90-%EB%A8%BC%EC%A0%80-data%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%9D%B4%EC%95%BC%EA%B8%B0%ED%95%B4%EB%B3%B4%EC%9E%90-d2e3ca2f3c2)
[카프카 프로듀서 (Kafka Producer)](https://always-kimkim.tistory.com/entry/kafka101-producer)
