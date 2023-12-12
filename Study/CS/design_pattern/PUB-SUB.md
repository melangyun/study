# Pub/Sub 의 구조

![pub-sub](https://velog.velcdn.com/images/haron/post/d433b364-a946-434d-b94b-96e4afb6400d/image.png)
1. 이벤트(메시지)를 발행하는 Publisher가 존재하며, Publisher는 특정 Channer(혹은 Topic)에 이벤트 전송한다.
2. 특정 Channel(혹은 Topic)을 구독하는 Subscriber가 존재하며, Publisher에 관계없이 발행된 이벤트를 받을 수 있다.

구체적인 발행/구독 방식이 서비스마다 다른데, 대표적으로 Kafka와 Redis가 있다.

## Kafka

![kafa](https://velog.velcdn.com/images/haron/post/683f3641-3416-4fec-a0eb-8539d158cc4d/image.png)
Kafka에서는 `Producer/Consumer`라는 개념이 등장한다. 
(각각 Publisher/Subscriber와 그 기능이 동일하다.)
Producer는 Topic에 이벤트를 보내고, 이 이벤트는 Topic의 각 Partition에 분산되어 저장된다.

Topic을 구독하고 있는 Consumer group내의 Consumer는 각각 1개 이상의 partition으로부터 이벤트를 가져온다. 
> 만약 partition 개수보다 consumer개수가 많다면, 아무 일도 하지 않는 consumer가 생기기 때문에, **항상 partition수를 consumer보다 같거나 크게 해주는 것이 좋다.**


## Redis

Redis에는 그룹이라는 개념이 존재하지 않고, 각 subscriber가 channel을 구독하고 있다.
이 때 중요한 점은, Channel은 이벤트를 저장하지 않는다는 것이다.
만일 Channel에 이벤트가 도착했을 때, 하댕 채널의 Subscriber가 존재하지 않는다면, 이벤트는 사라진다.


## kafka vs Redis

| 구분              | Kafka                                    | Redis                                                                    |     |     |
| ----------------- | ---------------------------------------- | ------------------------------------------------------------------------ | --- | --- |
| 이벤트의 저장여부 | 발행된 이벤트가 각 Partition에 저장된다. | 발행된 이벤트를 저장하지 않기 때문에, 구독자가 없다면 이벤트가 사라진다. |     |     |


1. 이벤트의 저장 여부
 Kafka는 발행된 이벤트가 각 Partition에 저장된다. 하지만 Redis는 발행된 이벤트를 저장하지 않기 때문에, 구독자가 없다면 해당 이벤트는 사라진다.
 따라서, 이벤트의 구독과 발행이 실시간으로 이루어져야 되는 상황인지, 혹은 언제든 발행된 이벤트를 읽으면 되는 상황인지에 따라 선택이 달라질 것이다.  
 메시지가 생성되었을 때 실시간 처리를 위해 Redis나 Memcached를 사용할 수 있다. 그러나 데이터를 메모리에 저장하기 때문에 장기간 보관하기엔 불안정하다. expired time이 지정되어 있지 않은 경우 메모리가 꽉 차면 문제가 생길 수 있다.

2. 한 이벤트를 받을 수 있는 Subscriber(Consumer) 개수  
	한 API에 대해, Scale-out 등의 이유로, 여러 서버가 작동될 수도 있다.
	
	앞선 예시를 생각해보자. Coupon 서비스는 유저 회원 가입에 대한 Topic을 구독하고 있고, 유저가 회원가입 했다는 이벤트를 받으면 회원가입 기념 쿠폰을 발행한다. 그리고 이때, Coupon 서비스에 대해 2개의 서버를 사용한다고 하자.
	![kafka를 사용한다면](https://velog.velcdn.com/images/haron/post/17d4d4a7-6bb3-4bb2-aaa9-2020333a4a43/image.png)
	만약 Kafka를 사용한다면, Consumer의 수와 관계없이, 유저 회원가입당 하나의 쿠폰이 발행될 것이다.  하지만, Redis 를 사용한다면?
	![redis를 사용할 때](https://velog.velcdn.com/images/haron/post/6dadeb3b-74f9-4e1a-b264-a5aa5a152462/image.png)
	 🤦‍♀️ 유저는 한 번의 회원가입으로 두 개의 쿠폰을 얻게 된다!  
	즉, 한 이벤트에 대해 한 번의 기능만 작동되어야 한다면 Kafka를 사용하는 것이 유리하다.  
	반대로 여러 서버에 모두 갱신되어야 할 데이터를 보내는 상황에서는 Redis를 사용하는 것이 적합할 것이다.  물론 Kafka에서도, 각 Process마다 다른 group Id를 부여하여 사용할 수도 있다.


---
[\[PUB\/SUB\] PUB/SUB을 파헤쳐보자](https://velog.io/@haron/PUBSUB-PUBSUB%EC%9D%84-%ED%8C%8C%ED%97%A4%EC%B3%90%EB%B3%B4%EC%9E%90)

