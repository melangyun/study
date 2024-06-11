분산된 시스템에서 이벤트 기반으로 통신하고 서로의 동작을 야기하는 패턴을 이벤트 기반 아키텍처라고 한다.

분산 아키텍처 환경에서 상호 간 결합도를 낮추기 위해 **비동기 방식으로 메시지를 전달하는 패턴**으로 주로 Message Broker(Kafka, RabbitMQ)와 결합하여 구성된다.

>[!tip] EDA는
>프로그래밍 관점뿐만아니라 다방면에서 적용가능한 아키텍처
>복잡성/역동성에 가장 효율적으로 대응가능하다. 이벤트를 통해 데이터간 연결이 생성된다는 점이 가장 중요하므로 **EDA에는 고정된 구조가 없다.**

## MSA와 이벤트 기반 아키텍처

MSA는 하나의 애플리케이션을 여러 서비스로 나누어 운영한다.
서비스들 간의 협업을 위해 **IPC(Inter Process Communication)**가  중요한 요소가 된다.

IPC는 RestApi, gRPC, 공유메모리, 이벤트 기반 통신 등 다양한 방법으로 구현 될 수 있다.
이 중 이벤트 기반 통신의 경우 비동기 방식이기 때문에, 동기 방식에 비해 서비스들 간 결합을 느슨하게 할 수 있다는 장점이 있다.

### 트랜잭션 관리

MSA에서는 별도의 DB를 가지고 있는 경우가 많은데, 데이터가 여러 DB에 분산되어 있다보니 데이터 간 일관성을 유지하는 것이 단일 DB에 비해 까다로운 편이다.
마이크로 서비스 아키텍처는 데이터 일관성을 유지하기 위해 일반적으로 사가([[saga]])패턴을 사용하는데, 이 패턴에서 이벤트가 활용된다.


# EDA의 구성요소

1. Event Generator (Publisher, Producer, Creater)
   표준화된 형식의 이벤트를 생성(발행)한다. 생성된 이벤트는 Event Channel로 전송.

2. Event Channel (Bus)
   Event Generator에서 Event Processing Engine으로 수집된 데이터를 전파하는 메커니즘
   > 이벤트를 필요로 하는 시스템까지 발송하는 역할

3. Event Processing Engine (Consumer, Processor)
   수신한 이벤트를 식별/처리하는 역할. 처리 결과에 따라 새로운 이벤트를 생성할 수 있다.
   Consumer는 이벤트의 송신자에 대한 정보를 알 필요가 없다.
   
![EDA의 구성요소](https://akasai.space/static/c281ca3843c645c19e735dd11a992999/c0b7e/eda_2.webp)


# EDA의 동작 방식

1. Message 생성(Publish/Subscribe)
	이벤트가 생성되면 `Subcribe(수신자)`에게 전달한다.
	이벤트는 반복 전달되지 않으며, <u>수신자는 송신자의 정보를 알 필요가 없다.</u>
2. Event Source  
    `Event Processor`에게 이벤트를 전달한다.
    `Event Source`는 1개 이상일 수 있으며, 1개 이상의 `Event Processor`에게 전달합니다.
3. Event Processor
    수신된 이벤트에 대한 여러 `Action`을 수행
    단일 이벤트에 대하여 타임스템프를 추가한다거나, 파생 이벤트를 만드는 등의 작업을 한다.
4. Event Consumer
    이벤트에 대한 처리를 합니다. 실질적인 **Biz Logic**을 수행한다.

# Event Procesing Style

^aba780

각 특징에 맞게 4가지로 구분된 Event Process Style이 있다.

1. Simple Event Processing
   각 이벤트가 직접적으로 수행할 `Action`과 매핑된다.
   일반적으로 실시간 **작업의 흐름(Flow of Work)** 을 처리할 때 사용한다.
   처리 시간과 비용이 적다.
2. Event Streaming Processing
	일반적인 이벤트와 중요한 이벤트가 모두 발생하며 이를 필터링하여 수신자에게 전달
	일반적으로 ==실시간 정보의 흐름==(Flow of Information) 을 처리할 때 사용한다.
3. Complex Event Processing
	일반적인 이벤트 패턴을 통해 복잡한 이벤트를 추론하는 방법입니다.
	예를 들면 일반적인 주식의 등락을 파악하여 투자할 타이밍을 추론할 수 있습니다.
4. Online Event Processing
    비동기 분산 이벤트 로그를 사용하여 복잡한 이벤트를 처리하며 지속해 데이터를 관리합니다.
    **높은 확정성과 일관성**을 가지며 유연하게 대처 가능한 패턴입니다.
    하지만 처리 시간을 보장할 수 없습니다.

## 토폴로지 구성

- `Broker Topology`: 일반적으로 한가지 작업만 필요한 단순한 단일 이벤트일 경우
- `Mediator Topology`: 이벤트 조율이 필요한 복잡한 이벤트 플로우일 경우

1. Mediator Topology (중재자 토폴로지)
	여러 단계의 과정을 중재자를 통해 조율할 필요성이 있으면 일반적으로 사용
	동시에 처리하지 않거나 실행 전에 처리해야 할 요소가 있으 사용하는 토폴로지이다.
	큐를 이용하여 사전처리를 진행한 후 관련된 `Consumer`에게 전달한다.
2. Broker Topology (브로커 토폴로지)
   **큐나 중재자 없이** 이벤트와 응답을 직접적으로 연관시키고자 할 때 사용합니다.
	이벤트 플로우가 단순한 중앙집중식 토폴로지이며 `Message Broker`와 `Consumer`가 가장 중요한 요소이다. 모든 작업은 비동기로 처리되며 <u>이벤트에 대한 조율이 필요 없다.</u>

# EDA 장단점

## 장점

1. 분산 시스템간 **느슨한 결합도**를 제공합니다.
2. 약속된 Message를 통해 통신하기 때문에 다른 시스템의 정보를 알 필요가 없으므로 시스템 간 의존성이 배제됩니다.
3. 확장성, 탄력성 향상

## 단점

1. 시스템 간 의존도는 낮아지지만 **메시지브로커에 대한 의존성**이 발생한다.
   만약 메시지 브로커의 장애가 발생하면 큰 장애로 확산될 가능성이 있음
2. Transaction 단위 분리
   장애나 이슈발생시 Retry/Rollback에 대한 고려가 필요하다.
3. 시스템 Flow 파악이 어렵다
4. 디버깅이 어렵다.



---
[EDA(Event Driven Architecture)이란?](https://akasai.space/architecture/about_event_driven_architecture/)
[Event Driven Architecture (이벤트 드리븐 아키텍처)란?](https://bsssss.tistory.com/1053)
