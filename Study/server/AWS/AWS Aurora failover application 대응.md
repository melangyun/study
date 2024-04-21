[[AWS Aurora Failover]] 와 [[aurora구조]] 에서 aurora의 구조와 failover에 대한 학습을 했다.
Aurora failover발생시 실제 발생하는 플로우와 대응해야 하는 로직들에 대한 정리를 해본다.

- Mysql에서 Aurora로 마이그레이션을 계획중이다.

[[failover발생시 흐름]] 을 보면 알 수 있듯, failover발생시 writer instance가 reader instance로 재시작되고, writer instance가 reader instance로 격상되는 과정이 존재한다.

이때, Cluster instance의 주소는 Primiray instane, 즉 writer instance를 가르키다가, 격상된 새로운 instance로 변경되는데 클라이언트(우리측 서버)는 DNS의 [[TTL]] 때문에 계속해서 기존 instance(reader 로격하된 instance)를 가르키게 된다.
- 때문에 TTL이 길게 설정되어있을 경우 CUD 요청시 계속해서 실패하게 된다.

따라서 failover 발생시 대응을 위하여 TTL을 그리 길지 않도록 설정하는것이 선행되어야 한다.
또, 어플리케이션 단에서는 TTL의 남은 시간동안, 발생하는 실패에 대응할 필요가 있다.

> cf) aurara의 DNS영역은 5초대로, 클라이언트에서 더 길게 늘리지 않는것이 권장된다.

- JVM 진영에서는 [스마트 드라이버 혹은 커넥터](https://docs.aws.amazon.com/whitepapers/latest/amazon-aurora-mysql-db-admin-handbook/using-smart-drivers.html)로 DB 메타데이터와 토폴로지를 읽어올 수 있다.
  이를 통해 클러스터 엔드포인트에 의존하지 않고, 개별 인스턴스 엔드포인트로 새 연결을 라우팅 할 수 있다.
  > 하지만 스마트 드라이버도 과도한 DNS 캐싱이 존재한다면 도움되지 않는다.

하지만 node진영에서는 스마트 드라이버가 지원되지 않는다.
따라서 어플리케이션 단에서 인스턴스가 reader로 격하 되었을 때에 발생하는 `innodb_read_only`옵션의 변화로 이를 구분하여 DB Connection을 재구성하는 대응이 필요하다.
- [Amazon Aurora DB 클러스터가 장애 조치된 후 읽기 전용 오류가 발생하는 이유는 무엇입니까?](https://repost.aws/ko/knowledge-center/aurora-mysql-db-cluser-read-only-error)

스마트 드라이버를 사용하지 않을 때에는 
```mysql
SELECT @@innodb_read_only;
```

질의를 통해 aurora 리더에 연결이 되어있는지 체크하며, `(reader의 경우 1, writer의 경우에는 0 을 반환)` 만일 failover발생으로 db연결이 reader와 맞물려있는 상황이라면 DB의 연결을 다시 구성할 필요가 있다.

## Sequelize hook을 이용한 대응
[sequlizeHook문서](https://sequelize.org/docs/v6/other-topics/hooks/)
Sequelize를 이용한 프로젝트에서는, Connection에 관련된 Hook이 존재한다. 따라서 `afterConnectionhook`에서 db에서 readonly option을 읽어와, 만일 readonly라면(reader에 엮여있다면) Connection을 끊는다.

> Connectoin이 끊어지면 ORM에서 Connection을 재시도 하며 DNS가 초기화 될 것이다.


## Typeorm 대응

typeorm은 table단위에서의 hook은 존재하지만, Database Connection hook은 존재하지 않는다.
따라서 nestJs에서 매 초마다 db의 readonly Option을 읽어오며, 만일 reader라면 `destroy` 이후 다시 `initialize` 과정을 거친다.

> 하지만, 매 초마다 쿼리를 요청하는것이 적합한지에 대한 의문은 있다. (오버헤드가 있지는 않을지에 대한 걱정)