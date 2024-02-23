![AWS_ALB_NLB](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*YuG-jq-PGFfiHlsI7daA2w.png)
# ELB(Elastic Load Balancer)

AWS에서 처음 출시한 로드밸런서. 현재는 `Classic Load Balancer`로 불림.
기본적인 로드 밸런싱 기능을 제공하여, 들어오는 트래픽을 여러 EC2 인스턴스에 분산시키는 역할을 한다.
HTTP, HTTPS, TCP, SSL과 같은 프로토콜을 지원

# ALB(Application Load Balancer)

보다 고급 애플리케이션 기반의 로드 밸런싱을 제공. HTTP, HTTPS 트래픽에 최적화 되어있으며, **경로 기반 라우팅, 호스트 기반 라우팅 등 고급 라우팅 옵션**을 제공
ALB는 마이크로 서비스와 컨테이너 기반의 애플리케이션에 적합함

## 경로 기반 라우팅
1. 단일 도메인에서 여러 마이크로 서비스를 호스팅 하는 경우.
	`/api`경로로 오는 요청을 api서버로, `/blog`경로로 오는 요청을 블로그 서버로 라우팅 할 수 있다.
2. A/B 테스팅 
	- `/v1`으로 오는 요청을 애플리케이션의 A버전
	- `/v2`로 오는 요청을 B버전으로 라우팅
3. 컨텐츠 기반 라우팅
	- 이미지, 비디오, 문서 등 미디어 파일 별도 처리 서버로요청을 라우팅
4. 블루 / 그린 배포

##  호스팅 기반 라우팅

HTTP 헤더의 호스트 필드 기반으로 클라이언트 요청을 여러 타깃 그룹에 분산시키는데 사용된다.
1. 다중 도메인 관리
	- `example.com`과 `api.example.com`으로 오는 요청을 각각 다른 타깃 그룹으로 라우팅하여, 각각의 서비스가 별도의 서버에서 처리되도록 할 수 있다.
2. 테넌트 기반 멀티테넌시 애플리케이션
	- SaaS애플리케이션에서 각 태넌트를 위한 독립된 서브 도메인을 제공할 때 유용
	- `customer1.example.com`,`customer2.example.com` 으로 오는 요청을 각 고객의 전용 서버로 라우팅 해줄 수 있음
3. 환경 분리
	- 개발, 테스트, 프로덕션 등 다양한 환경을 운영하는 경우 호스트 기반 라우팅을 통해 각 환경에 대한 요청을 별도 타깃 그룹으로 라우팅함으로서 환경 간 격리를 강화할 수 있다.
4. 리소스 최적화
	- 여러 웹/애플리케이션을 같은 인프라상에 운영하면서도 각각의 트래픽을 효과적으로 관리하고 분산시킬 수 있다.

# NLB(Network Load Balancer)

높은 성능과 낮은 지연시간이 요구되는 TCP 트래픽에 최적화된 로드밸런서. 4계층 (TCP/UDP)에서 작동하며, 수백만 개의 요청을 초 단위로 처리할 수 있다.
NLB는 정적 IP주소를 할당받을 수 있고, AWS내 또는 온프레미스 서버로 트래픽을 라우팅할 수 있는 기능을 제공

- 간단한 로드 분산 -> ELB
- 애플리케이션 수준에서 고급 라우팅 기술이 필요한 경우 -> ALB
- 매우 높은 성능이 요구되는 경우 -> NLB

> Docker 컨테이너를 배포하고 로드 밸런서를 사용하여 네트워크 트래픽을 보내는 경우 Ec2 컨테이너 서비스는 ALB와 NLB를 둘 다 제공


# ALB vs NLB
- OSI계층 (7계층 / 4계층)
- Routing
	- NLB는 요청을 전단하는 반면 ALB는 HTTP 헤더의 내용을 검사하여 요청을 라우팅할 위치를 결정함.
- Static IP
	- ALB는 고정 IP주소를 지원하지 않음
	- NLB는 고정 IP주소를 지원함.
- PrivateLink(Endpoint services)
	- NLB는 VPC엔드포인트 서비스 통합을 통해 Private Link를 지원하지만, ALB는 Private Link를 지원하지 않는다.
		-> NLB만 PrivateLink로 직접 사용가능
- 애플리케이션 가용성
	- NLB는 애플리케이션 가용성을 보장할 수 없다.
		TCP 계층 변수에만 결정을 내리고 애플리케이션을 전혀 인식하지 못하기 때문.
		일반적으로 NLB는 ICMP Ping에 응답하거나 3way Handshake를 올바르게 응답하는 서버의 능력을 기반으로 가용성을 결정함.
	- ALB는 훨씬 더 깊이 들어가 특정 페이지의 성공적인 HTTP Get 뿐만 아니라 입력 매개변수를 기반으로 콘텐츠가 예상대로인지 확인하여 가용성을 결정할 수 있다.
- IP 주소를 공유하는 동일한 호스트에 여러 애플리케이션의 배포를 고려할때 NLB는 포트가 다르지 않다면 애플리케이션을 구분할 수 없지만, ALB는 여러 애플리케이션을 구분한다.




---
[AWS — Difference between Application load balancer (ALB) and Network load balancer (NLB)](https://medium.com/awesome-cloud/aws-difference-between-application-load-balancer-and-network-load-balancer-cb8b6cd296a4)