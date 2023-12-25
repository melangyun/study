# 서버 켜기

## 주키퍼

```bash
/opt/homebrew/bin/zookeeper-server-start /opt/homebrew/etc/zookeeper/zoo.cfg
```

## 카프카

```shell
/opt/homebrew/bin/kafka-server-start /opt/homebrew/etc/kafka/server.properties
```


# 토픽 생성하기

```bash
/opt/homebrew/bin/kafka-topics --create --topic topic-example1 --bootstrap-server localhost:9092
```

# 주요한 토픽 보기

```bash
/opt/homebrew/bin/kafka-topics --describe --topic topic-example1 --bootstrap-server localhost:9092
```

```Pain Text
Topic: topic-example1	TopicId: zFXqNM-eRBCeRXV6oamM9Q	PartitionCount: 1	ReplicationFactor: 1	Configs:
	Topic: topic-example1	Partition: 0	Leader: 0	Replicas: 0	Isr: 0
```

## 프로듀서를 통해 메세지 발행

```bash
/opt/homebrew/bin/kafka-console-producer --topic topic-example1 --bootstrap-server localhost:9092
```

### 해당 명령어를 통해 읽어올 수 있음

```bash
/opt/homebrew/bin/kafka-console-consumer --topic topic-example1 --from-beginning --bootstrap-server localhost:9092
```


---
https://velog.io/@haerong22/Apache-Kafka-CLI-%EA%B8%B0%EB%B3%B8-%EC%82%AC%EC%9A%A9%EB%B2%95

[[Kafka]]
