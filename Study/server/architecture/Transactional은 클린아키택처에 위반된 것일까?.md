얼마전 이러한 질문을 받았고, 이에 대해서 생각해본 적이 없던 나는 인프라 영역이지만, 어플리케이션단에 침해된(?)것이 아닐까요? 라고 답변했다.

하지만 돌이켜 생각해보니, 세부 구현은 인프라계층에 존재하며, 트랜잭션 경계 설정과 같은 제어는 어플리케이션 단에 포함될 수 있으며, 클린아키텍처에 위반되지 않는다는 생각이 든다.

DB관련된 작업은 보통 인프라에서 처리되며, 사비스는 이를 호출할 뿐이다. 따라서 인프라에 의존하는 것은 자연스럽다. 서비스 계층은 애플리케이션의 비즈니스 로직을 포함하며, 이 로직이 트랜잭션으로 묶여야 하는 경우가 많다. 따라서 비즈니스 로직을 실행하는 도중에 트랜잭션이 필요한 경우 Transactional로 사용하는것은 적합하다.