# 비동기 메시지 패턴(Asynchronous Messaging Pattern)

비동기 메세징은 확장성과 안정성, 성능 향상을 목적으로  발행자(producer)의 메세지 생성이 구독자(consumer)의 작업과 분리되는 방식이다.
메세징 시스템을 다룰 때, 일반적으로 Message Queue와 Publish/Subscribe 2가지로 나뉜다.

## Message Queues
Message Queue는, 메세지를 만드는 발행자(publisher)와 메세지를 보관하고 있는 큐(Queue), 큐에서 메세지를 소비하는 여러개의 소비자(consumer)로 이루어져 있다.
  
이 통신 방식은 publisher가 consumer에게 명령을 내리는 방식으로 작동한다.
publishing 서비스는 메세지를 큐 혹은 exchange에 넣고, 1개의 consumer Service가 이 명령에 따른 동작으로 메세지를 소비한다.

![큐1](https://www.baeldung.com/wp-content/uploads/2021/07/1-1.png)
- 오른쪽에  consumer A가 m1 메세지를 읽는다
- consumer A가 소비했기 때문에, 이 메세지는 consumer B에서는 소비 할 수 없다.

![message_queue1-2](https://www.baeldung.com/wp-content/uploads/2021/07/2-1.png)
Message queue는 메세지 처리 작업을 소비자에게 위임한다. 따라서, 작업이 한 번만 실행되도록 할 수 있다.

Message queue는 MSA에서 많이 사용된다.  클라우드 기반 또는 서버리스 애플리케이션을 개발할 때 부하에 따라 앱을 scale 할 수 있다. 예를 들어, 큐에 처리되어야 할 많은 메세지들이 있다면, 같은 메세지 큐를 listen하는 여러개의 소비자들을 추가 할 수 있다. 메세지가 빨리 처리된다면, 트래픽이 적을 때는 비용을 절약하기 위해서 소비자를 종료 될 수도 있다.

## Pub-Sub
Pub-sub에서, 모든 구독자(subscriber)는 발행자(publisher)가 exchange에 전송하는 메세지 복사본을 1개 이상 가진다.
![pub-sub](https://www.baeldung.com/wp-content/uploads/2021/07/3-1-1536x386.png)
 이 Topic은 이 메세지를 구독자(subscriber)들에게 브로드캐스트로 전송합니다. 이 메세지들은 <u>큐에 보내지고</u>, 각 큐는 메세지를 listen하고 있는 구독자(subscriber) 서비스를 가지고 있습니다.

![pubsub-1-2](https://www.baeldung.com/wp-content/uploads/2021/07/4-1536x386.png)

- 2개의 구독자(subscriber)는 모두 "m 1" 메세지를 소비(consume)한다.
  또한, Topic이 새로운 메세지 "m n+1"을 모든 구독자(subscriber)에게 복사하여 분배한다
  
  Pub-Sub은 모든 구독자(subscriber)들이 메세지의 복사본을 가지도록 보증할 때 사용한다.



 > [!check] Message Queue와 Pub-Sub 구조 모두 어플리케이션의 수평확장을 위해서 훌륭한 방법이다

  
 또한 전통적인 동기 방식보다 훨씬 **지속성(durability)**이 좋다.
 예를 들어, 만약에 앱 A가 HTTP로 앱 B에 비동기 통신을 보냈고, 앱이 다운되었다면, 데이터는 유실되고 다시 요청을 보내야 한다.

Message Queue를 사용하면 consumer 앱이 다운되더라도, 다른 consumer가 메세지를 대신 관리할 수 있습니다.  Pub-Sub를 사용하면, 구독자(subscriber)가 다운되더라도, 손실된 메세지를 복구하면 토픽에서 사용할 수 있다.

> 2개 방식 중 하나를 선택하는 핵심 기준은 **"모든 consumer들이 모든 메세지를 전부 수신해야하는가?"** 


> [!info] Message Queue vs Message Broker 차이는?  
  Message queue는 queue를 사용해 데이터의 전송, 수신 저장하는 어플리케이션들의 통신에 책임을 진다. message queue를 통해 데이터가 전달되지만, 이 데이터들의 내용을 전혀 알지 못합니다.  
  > 
  Message broker는 message queue의 사용을 상속하는 메커니즘으로, message queue와는 달리 관리되는 데이터들의 정보를 알고 있다.
  >
 즉, message queue는 발행되고 소비되는 데이터를 저장하는 구조이고, message borker는 message queue를 관리하는 소프트웨어 컴포넌트에 가깝습니다.

---
[Message Queues vs Pub/Sub](https://escapefromcoding.tistory.com/706)
[[PUB-SUB]]