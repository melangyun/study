Aurora는 Mysql과 PostgreSQL과 호환되는 성능을 제공한다.
- Aurora PostgreSQL

> [!tip] AZ(Availiablilty Zone)
> Availiability Zone (가용영역) -> AWS의 데이터 센터가 위치한 지리적인 영역을 의미
> - 하나의 리전 내에 위치한 서로 격리된 데이터 센터 그룹
> - 독립된 전력, 냉각, 보안 등의 인프라를 갖추고 있어, 하나의 AZ에서 문제가 발생해도 다른 AZ의 리소스는 영향을 받지 않는다.
> - 높은 가용성과 장애 허용성 제공

멀티 AZ는  DB의 고가용성과 내구성을 보장하기 위해 설계되었다. 이 구성에서는 데이터베이스가 여러 가용영역 (AZ)에 걸쳐 복제된다. 주요 목적은 하나의 AZ에 장애가 발생해도 데이터베이스 서비스가 중단되지 않도록 하는것.

---

오로라는 Read Replica를 Failover에 사용한다. 여러 RR(`Read Replica`)이 같은 클러스터로 묶여있고, Write 권한이 있는 마스터가 다운되면 RR중 하나를 마스터로 자동 승격시켜 대응한다.

> [!tip] failover 과정은 수초 내로 기존 RDB대비 굉장히 빨리 이루어진다.
> 이는 Storage 가 Computation Unit과 물리적으로 분리되어 있으며, DNS 차원에서 연결을 승격된 RR로 바로 틀 수 있기 때문이다.


> 기존의 RDB는 Computation과 Storage를 단일 VM에 모두 지닐수밖에 없어 빠르게 Failover하는것이 힘들었다. 그리고  DB의 Endpoint는 master instance에 직접 연결되어 있는 주소였기 때문에 master에 장애가 생기면 이를 수동으로 RR과 교체해줄때 까지 서비스에 문제가 생기는 것은 감수해야 했다.

하지만 Aurora의 Storage는 Computation과 물리적으로 분리되어 여러 AZ에 걸쳐 복제되어있다.
따라서 Aurora에선 Computation instance는 언제든 문제가 생기면 클러스터 내의 다른것으로 빨리 갈아버린다.

![Computing instance 와 Storage는 따로국밥](https://miro.medium.com/v2/resize:fit:1300/format:webp/1*D3LlqpLiRkEo8gJ_YQkQmg.png)


그렇기 때문에 Aurora Instance에 안정적으로 접속하고 싶다면 마스터 외에 1개 이상 RR 붙여주어야 한다.


## 클러스터와 인스턴스

Aurora에선 Failover와 관련된 Operation 부터 클러스터 기반으로 돌아간다. 따라서 클러스터를 쓸건지 인스턴스만 쓸건지 결정할 수 있는 다른 엔진과 달리 반드시 클러스터를 생성해야 한다.
- Cluster Endpoint와 Instance Endpoint가 각각 주어지며, 인스턴스가 하나도 없어도 Cluster Endpoint가 존재한다.

사용자들이 Write Query를 날리고싶다면 `Cluster Endpoint`에 날려야 하며, 이 Endpoint는 master = primary instance로 연결된다. 
> 인스턴스 레벨의 Endpoint는 각각의 인스턴스에 접근할 수 있는것처럼 보이지만 장애시 CNAME Swapping을 위해서 존재하는 주소로서의 역할이 크다.

또한 Reader Endpoint라는 Endpoint도 클러스터 레벨에서 지원하는데, 이 Endpoint로 들어온 트래픽은 클러스터 내의 여러 Read Replica 에게 Load Balancing된다. 따라서 웹 서버에서는 Write는 Cluster Endpoint로 설정하고, Read Replica접근은 Reader Endpoint로만 가도록 만들면 된다.



---
[aws-rds-aurora-faqs](https://aws.amazon.com/ko/rds/aurora/faqs/)
[AWS Aurora 도입전에 알아야 할 몇가지 사실](https://aws.amazon.com/ko/rds/aurora/faqs/)
[\[AWS\] Aurora의 자가 복구 분산 스토리지](https://velog.io/@combi_areum/AWS-Aurora%EC%9D%98-%EC%9E%90%EA%B0%80-%EB%B3%B5%EA%B5%AC-%EB%B6%84%EC%82%B0-%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80)
<iframe width="560" height="315" src="https://www.youtube.com/embed/RImUPhD8X-o?si=jJd9OyAJLrmtUPVm" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
