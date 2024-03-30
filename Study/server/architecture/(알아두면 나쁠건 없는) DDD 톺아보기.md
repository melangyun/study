많이 헷갈리는 것 중 하나는, DDD는 `Domain Driven Development`가 아니라, `Domain Driven Design` 입니다.
- `개발`보다는 `설계`접근 방식이지만, 코드에 맞닿아 있는 개발자들이기 때문에 잊기 쉬운것같습니다.
![[DDD는 Design이다.png]]

> DDD는 복잡한 요구사항을 가진 소프트웨어 모델링을
> 현실세계의 도메인(문제영역)과 긴밀히 연결하여 개발하는 설계 철학입니다.

# 전략적 설계, 전술적 설계

DDD의 설계는 `전략적 설계`, `전술적 설계` 크게 두가지 접근방식을 사용합니다.

|       |                전략적 설계                 |          전술적 설계           |
| :---: | :-----------------------------------: | :-----------------------: |
|  범위   |                  전반적                  |    특정 Bounded-Context     |
|  목적   |            문제 도메인을 해결영역으로             |       풍부한 도메인 모델 적용       |
|  메타포  |                전쟁에서 전략                |          전투에서 전술          |
| 수행방식  |                  접근법                  |         방법론에 가까움          |
| 주요 패턴 | Bounded-Context<br>Ubiqutous-Language | Aggregate<br>Domain Event |

전략적 설계는 전체적 범위에서 문제 도메인을 해결 영역으로 나누는 것을 목표로 합니다. 이는 전쟁에서의 전략과 비슷하다고 볼 수 있을것 같습니다.
전술적 설계는 특정 Bounded-Context내에서 디테일한 도메인 모델을 적용하는 것을 목표로 합니다.

# 전략적 설계

전략적 설계는 앞서 설명했듯, 현실의 문제 영역을 명확하게 파악하고 분석하는것 부터 시작합니다.
문제 영역을 정확히 파악하는것은 유비쿼터스 언어를 정하는것이 시작으로 볼수도 있을것같습니다.

## 유비쿼터스 언어 - Ubiquitous Language

> [!cite] 유비 쿼터스언어
> >사례: [MSA 에서 유비쿼터스 언어(보편 언어)의 중요성](https://medium.com/dtevangelist/msa-%EC%97%90%EC%84%9C-%EC%9C%A0%EB%B9%84%EC%BF%BC%ED%84%B0%EC%8A%A4-%EC%96%B8%EC%96%B4-%EB%B3%B4%ED%8E%B8-%EC%96%B8%EC%96%B4-%EC%9D%98-%EC%A4%91%EC%9A%94%EC%84%B1-ca22b96aaeea)
>
>- `Reward` 가 사용자에게 주어지면, 사용자 입장에서는 `Item`인가?
>- 운동을 안해서 주는 경고도 `Reward`인가?
>- 내가 운동을 많이 했다고 (선물이 아닌) 칭찬 메시지가 오는것도 `Reward` 인가?
>- 친구가 나를 역전했다고 알려주는것도 `Reward`인가?
>---
>- 챌린지와 목표의 차이는?
>- 챌린지가 이벤트랑은 다른걸까?
>-  챌린지를 집단으로 하면 챌린지인가 이벤트인가?

이런 모호한 상황에서

> "이벤트 리워드는 (\~~)가 될것같다.."

라는 이야기가 나오면 정말 수많은 이야기로 해석할수있습니다.


![뭐라는거야..](https://blog.tekaris.com/wp-content/uploads/2019/03/image-507x321.png)


같은 의미로 내뱉는 말들이 각기 다르고, 똑같은 말로 들리는데 의도가 다릅니다.
- [?] 이 명확히 확인되지 않은 언어들로, API를 구현하고 DB Table을 정의하게 된다면? 💦💦

개발단에서 설계 뿐만아니라, 실제로 프로젝트 진행의 병목지점이 되기도 하며, 조직에서 의사소통 비용이 너무 큽니다.
이를 타파하기 위해 유비쿼터스 언어를 정하고 사용합니다.

![uniquitous language](https://miro.medium.com/v2/resize:fit:877/1*EyEEkDaoezAVHhEobyTFgw.png)

- 개발자만이 아닌, 개발자, 아키텍트, 도메인 전문가, 디자이너 등등 `모두가 모여` 의도가 정확히 전달되는 유비쿼터스 언어(보편언어)를 합의하고 정의해야 합니다.

> (기술 + 비즈니스 용어)
> 개발자 뿐만아니라 모두가 이해하고 동일한 것을 바라볼 수 있는 언어를 정해야한다.
> 사소한 영역까지 모두 구체화 해야함

이렇게 정해진 유비쿼터스 언어는 의사소통을 할때에도, 문서 작성을 할때도, 실제 코드 깊숙히까지 들어가게 되는 언어가 됩니다.

모호했던 부분을 구체화하고, 유비쿼터스 언어를 정해가면, 도메인은 점차 명확해지게 됩니다.

> [!cite] 유비쿼터스 언어는 왜 중요할까
> A domain is often a complex collection of variables in a set environment that can shrink, expand and evolve — depending on how you define the boundaries. For complex environments you can’t sit down and write code without understanding the essence of it.
> 도메인은 경계를 정의하는 방법에 따라 축소, 확장, 진화할수 있는 변수들의 집합이다. 복잡한 환경에서는 코드의 본질을 이해하지 못하고 코드를 쓸 수 없다.


## 도메인을 정하고 나누기

- 사용 사례 (use-case)분석
- 이벤트 스토밍
- Business Model 분석


![1단계](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*zXa4hw1MA20GCNIBMt7GoQ.jpeg)

![2단계](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*2vLXUDIhwuB6SLIp5WZlNw.jpeg)

![3단계](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*mhot7hJTOCY61cPw9mvpKA.jpeg)

![4단계 뭣이 중헌디](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*DqrdQqyJFdk_fbgG4v7t4A.jpeg)

>[!important] 중요한것과 중요하지 않은 것은 무엇인가?
>- 핵심 도메인을 판별하는것이 `문제 공간`을 판별하는 목적
>> 핵심 -> 경쟁사에 비해 우위를 가질 수 있는것
>
>핵심은 내부에서 개발하고, 핵심이 아닌것은 상품으로 이용하거나, 외부 개발을 하는것도 방법이 됩니다.

## context Map

> 바운디드 컨텍스트?

나눈 컨텍스트 간의 관계도를 그립니다. 이를 `Context Map`이라고 합니다.
연결방법 및 정보의 흐름, 의존성의 방향 등이 드러나게 됩니다. (upstream, downstream)

![context-map](https://raw.githubusercontent.com/ContextMapper/context-map-generator/master/examples/context-map-example-1.png)

> 설계단계에서 컨텍스트 맵이 명확하지 않을경우 순환참조나, 의존성 문제, 중복 로직의 문제가 생길수 있습니다.
> - 이후 통합의 문제로 이어짐


> [!question] 어쩌면 DDD.. 멀리있지 않을지도? 🤔

# 전술적 설계 (구현)

개별 컨텍스트 내에서 어떻게 모델링하고 구현할것인가?

![도메인 설계도](https://user-images.githubusercontent.com/42582516/150660566-f6ed55db-7b57-408e-b624-ddf3c87d9552.png)

![루드엔티티](https://blog.kakaocdn.net/dn/9HiGG/btrN28J9KSt/dh1RMRsVjnnYNGztxZEF5K/img.png)

> 도메인 설계 -> 실제 서버는 어떤식으로 구현할까?

- (크게봤을때 )`layered Architecture` 혹은 `clean Architecture` 중심으로
![서비스 흐름](https://velog.velcdn.com/images/pjh1011409/post/7251ffdf-498f-4ec5-b200-c1c834be6c64/image.png)
![의존성의 방향](https://miro.medium.com/v2/resize:fit:1400/0*v2EisG6QUMmr7e4G)


- 헥사고날은 선택의 영역
![헥사고날](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbSBinD%2FbtrlZuAWOpH%2FmnhzGhWJR7ijQmFXK7au8K%2Fimg.png)

- `도메인` 중심이기 때문에 transaction의 제어 단위는 Aggregate가 가져간다고 생각하면됨
- 접근 지점은 Aggregate -> 캡슐화
- `느슨한 결합`과 `높은 응집도` 를 강조하기 하기때문에 EDA도 함께.. 

>[!example] 유저 회원가입 플로우
>1. 유저 Interface 통한 회원가입요청이 들어옴
>2. service(응용계층)에서 비즈니스 로직 + 도메인 호출
>3. Domain에서 domain 로직이 수행됨
>4. database save 와 함께 `user.created 도메인 이벤트` 발행
>5. 이를 구독하고 있는 다른 도메인에서 수신하여 액션


- CQRS, Event Sourcing.. 끝도 없는데 전술적 설계는 방법론이자 선택의 영역입니다.
	- 적절한 영역에 적절한 방식으로 선택적으로 합리적으로 반영하는것이 중요합니다.
# 언제하는게 좋을까?

![DDD추천 영역](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*7hfGxerrsQbpL7Oa15JfbQ.jpeg)

 ![Big ball of Mud](https://miro.medium.com/v2/resize:fit:1200/0*EWjybLwJbxllHPFo)

 - 많이 복잡한 도메인영역.
 - 간단한 도메인이면 당연히 <u>안하는게</u> 전략이다.
 -  SW가 Bigball of mud 스타일에서 방대한 복잡성을 감당할 수 없지만, 개선의지가 있을때 적용하면 좋다.

소프트웨어가 얼만큼 복잡해질지 모르는 상황에서 서비스 초기단계부터 DDD를 적용하는것은 도움이 되지 않는다. 미래는 예측 불가능한 영역이기 때문에.
- 도메인의 요구사항도 계속해서 바뀌고 분명 생명 주기가 있기 때문에 섯불리 먼저 적용하면 망해버리는 이유가 되기도 할듯



---
<발표자료>
[Part 1: Domain Driven Design like a pro 🏅](https://medium.com/raa-labs/part-1-domain-driven-design-like-a-pro-f9e78d081f10) 
[[NHN FORWARD - DDD 뭣이 중헌디]]
