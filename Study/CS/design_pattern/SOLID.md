# 객체 지향 설계의 5원칙 (S.O.L.I.D)

SOLID 원칙이란 객체지향 설계에서 지켜줘야 할 5가지 소프트웨어 개발 원칙을 말한다.
- SRP(Single Responsibility Prinicple): 단일 책임 원칙
- OCP(Open Closed Principle): 개방 폐쇄 원칙
- LSP(Listov Substitution Principle): 리스코프 치환 원칙
- ISP(Interface Segregation Principle): 인터페이스 분리 원칙
- DIP(Dependency Inversion Principle): 의존 역전 원칙

> [!tip] 좋은 설계란?
> 시스템에 새로운 요구사항이나 변경 사항이 있을 때, 영향을 받는 범위가 적은 구조.
> 시스템이 예상하지 못한 변경사항이 발생하더라도, 유연하게 대처하고 확장성 있는 시스템 구조를 만들 수 있다.
> >여러 디자인 패턴들이 SOLID설계 원칙에 입각해서 만들어 진 것이기 때문에, 표준화 작업부터, 아키텍처 설계에 이르기까지 다양하게 적용되는 근간이 되는 SOLID에 대해 탄탄하게 알아볼 필요가 있다.

> [!info] 좋은 소프트웨어란 변화에 대응을 잘 하는것!

> [!question] 반드시 5원칙을 다 적용해야 할까?
> 코드의 구성에 따라 다르다. 각 원칙은 특정 문제를 해결하기 위한 지침일 뿐이다.
> 해당 코드에 문제가 없다면 원칙을 적용하지 않아도 된다.

# 단일 책임 원칙 - SRP (Single Responsibility Principle)

![SRP](https://blog.kakaocdn.net/dn/xumrV/btrORP3OSF3/2lqQO1FiD5mo2OTxUPgfy1/img.png)

- 객체는 단 하나의 책임만 가져야 한다.
- 하나의 클래스는 하나의 기능을 담당하여 하나의 책임을 수행하는데 집중되어야 한다.

# 개방 폐쇄 원칙 - OCP (Open Closed Principle)

![OCP](https://blog.kakaocdn.net/dn/cI4aY1/btrOSkPrtK1/xAANQRF6KijsiBb2bcyOX1/img.png)

- 확장에는 열려있어야 하며, 수정에는 닫혀있어야 한다.
- 기능 추가 요청이 오면 클래스를 확장을 통해 손쉽게 구현하면서, 확장에 따른 클래스 수정은 최소화 해야한다.
- OCP 추상화를 통한 관계 구축을 권장
- 다형성과 확장

# 리스코프 치환 원칙 - LSP (Liskov Substitution Principle)

![LSP](https://blog.kakaocdn.net/dn/GQ4OQ/btrOSa0eNP0/r73k2jQOTj3fQtpRT4D0Uk/img.png)

- 서브타입은 언제나 부모타입으로 교체할 수 있어야 한다.
- 다형성의 원리를 이용하기 위한 원칙
- 다형성의 특징을 이용하기 위해 상위 클래스 타입으로 객체를 선언하여 하위 클래스의 인스턴스를 받으면, 업캐스팅된 상태에서 부모의 메서드를 사용해도 동작이 의도대로 흘러가야한다는 것을 의미


# 인터페이스 분리 원칙 - ISP (Interface Segregation Principle)

![ISP](https://blog.kakaocdn.net/dn/mRSwQ/btrORX1toTn/uK0svKUNfO1CViSqabphKK/img.png)

- 인터페이스를 각각 사용에 맞게 잘 분리해야한다는 설계 원칙
- SRP원칙이 클래스의 단일 책임이 강조한다면, ISP는 인터페이스의 단일 책임을 강조하는 것이다.
- SRP원칙의 목표는 클래스 분리를 통해 이루어진다면, ISP원칙은 인터페이스 분리를 통해 설계하는 원칙이다.
- ISP 원칙은 인터페이스를 사용하는 클라이언트를 기준으로 분리함으로써, 클라이언트의 목적과 용도에 적합한 인터페이스를 제공하는것이 목표이다.

# 의존 역전 원칙 - DIP (Dependency Inversion Principle)

![DIP](https://blog.kakaocdn.net/dn/dagTxZ/btrOS2asN0X/4Sl2vLTkjUS9fCwGt6Jt51/img.png)

- 구현 클래스에 의존하지 말고, 인터페이스에 의존하라
- 의존 관계를 맺을 때 변화하기 쉬운것, 또는 자주 변화하는것 보다는 변화하기 어려운것, 거의 변화가 없는것에 의존하라

> 고수준 모듈이 저수준 모듈에 의존해서는 안된다.

---
[💠 객체 지향 설계의 5가지 원칙 - S.O.L.I.D](https://inpa.tistory.com/entry/OOP-%F0%9F%92%A0-%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%EC%84%A4%EA%B3%84%EC%9D%98-5%EA%B0%80%EC%A7%80-%EC%9B%90%EC%B9%99-SOLID)