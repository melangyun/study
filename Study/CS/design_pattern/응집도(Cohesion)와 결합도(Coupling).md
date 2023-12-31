
> [!info] 모듈
> 여기에서 의미하는 모듈은 크기와 상관없이 클래스나 패키지, 라이브러리와 같이 프로그램을 구성하는 임의의 요소
> 
> 참고로 클린 소프트웨어 저자인 로버트 마틴에 따르면 **모든 모듈**은 **1. 제대로 실행**되어야 하고, **2.변경이 용이**해야되고, **3. 이해하기 쉬워야 한다**고 한다.

# 응집도(Cohension)
응집도`Cohesion`는 모듈에 포함된 내부 요소들이 `하나의 책임/목적`을 위해 <u>연결되어있는 연관된 정도</u> 이다.
- 모듈이 하나의 목적을 수행하는 요소들간의 연관성 척도
- 모듈 내부의 기능적인 응집 정도를 나타냄

- [*] **응집도가 높으면, 변경 대상과 범위가 명확해지는 장점이 있어서 코드를 수정하기 쉬워진다.**
- [*]  응집도가 높으면 복잡도가 낮아진다.
	- [p] 하나의 모듈에 하나의 책임을 위해 연결이 잘 모여있는것
	- [c] 퍼저있는것

![높은 응집도](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*LEWcq_PgKW6LvLb7SezUdQ.png)
> - 높은 응집도
> - 기능 a에 관련된것은 모두 A모율에 위치해있다.
![낮은응집도](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*RcUn_fKNhAfQ0K0QAckClw.png)
> - 낮은 응집도
> - 기능 a에 대한것이 퍼져있다

>[!tip] 응집도가 높다 vs 낮다
>A 모듈 안에 a 라는 기능을 위해 모여있고 긴밀하게 연결되어 협력하고 있다면 그 모듈은 높은 응집도를 가진다 할 수 있다.
>그 반대로 *서로 다른 목적을 가지고 있거나, 흩어져 있다면 낮은 응집도를 가진다 할 수있다.*

>[!warning] 응집도가 높으면 무조건 좋을까?🤔
>응집도가 높으면 수정해야될 코드가 한군데 모여있기 때문에 최소한의 모듈만 분석해서 수정하면 되니 _유지보수 하기 좋을것._
> - [c] 올바르지 않은 위치에 코드가 모여있는 경우
> - [c] 서로 다른 책임의 코드를 하나의 모듈에 뭉쳐두고, 그 중 하나의 코드에 변경해야 하는 상황이 발생한 경우


# 결합도(Coupling)

다른 모듈과의 의존성 정도. 모듈 수정을 위해 다른 모듈의 변경을 요구하는 정도

- **모듈이 다른 모듈에 의존하는 정도의 척도**
- **모듈과 모듈간의 상호 결합 정도를 나타냄**

- [*] **결합도가 낮으면, 검토해야 하는 소스의 수가 적어져서 코드의 수를 수정하기 쉬워진다.**
	- [p] 하나의 모듈에 하나의 책임을 위해 연결이 잘 모여있는것
	- [c] 퍼저있는것

![낮은 결합도, 높은 결합도](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*9fOHc8tRHeiOSYUS_oMd2w.png)

- A모듈: '느슨하게 연결되었다'고 표현. 결합도가 낮음
- B모듈: 기능 b를 수정하기위해서 DEFI모듈을 모두 수정해야함 => 결합도가 높음
---
> [!tip] 결합도, 응집도의 강함 약함의 척도
> - 응집도 (강함⬅️ ➡️약함) : 기능적, 순차적, 교환적, 절차적, 시작적(일시적) , 논리적, 우연적 응집도
> - 결합도 (약함⬅️ ➡️강함) : 자료, 스탬프, 제어, 외부, 공통, 내용 결합도

- [*] 인터페이스에 의존하는 코드 작성은 낮은 결합도를 얻을 수 있다

---
[\[설계 용어\] 응집도\(Cohesion\)와 결합도\(Coupling\)](https://medium.com/@jang.wangsu/%EC%84%A4%EA%B3%84-%EC%9A%A9%EC%96%B4-%EC%9D%91%EC%A7%91%EB%8F%84%EC%99%80-%EA%B2%B0%ED%95%A9%EB%8F%84-b5e2b7b210ff)
