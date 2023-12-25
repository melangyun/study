각 메시지가 모든 컨슈머에 전달된다.
컨슈머가 브로드캐스팅된 동일한 메시지를 서로 간섭없이 들을 수 있다.

## 카프카

카프카의 경우 컨슘될 때 카프카에서 메시지가 제거되지 않아서 소비자를 여럿 추가할 수 있고, <u>각 컨슈머는 자체 메시지 오프셋을 관리할 수 있다.</u> (물론 컨슈머는 서로 다른 컨슈머 그룹에 있어야 한다.)

> [!tip] [참고] 로드밸런싱
> 각 메시지는 여러 컨슈머 중 특정 컨슈머에 전달된다.
>브로커는 메시지를 전달할 컨슈머를 임의로 지정한다.
>이 패턴은 메시지를처리하는 비용이 비싸서 처리를 병렬화 하기위해 컨슈머를 추가하고 싶을 때 유용.
>또, 컨슈머가 죽으면 관련 컨슈머 그룹에서 나머지 실시간 컨슈머에게 나누어진다.

## SNS + SQS

![SNS+SQS](https://blog.kakaocdn.net/dn/k90ph/btrAgpEPeOU/pwmNkBfU8GXajObyVR9xa1/img.png)

여러 SQS 대기열에 메시지를 보내고 싶을 때 모든 SQS대기열에 게뱔적으로 메시지를 전달하면 문제가 발생할 수 있다. 따라서 여러 SQS에 메시지를 보내고 싶을때는 FanOut 패턴을 이용하는 것이 좋다.

- 각각의 대기열에 메시지를 전달하는 것이 아니라, SNS Topic에 해당 메시지를 전달한다.
- Topic을 메시지가 전달하려고 하는 대기열이 구독한다.

이러한 FanOut Pattern을 사용하면 쉽게 SQS대기열로 전송할 수 있고, 데이터 지속성, 지연처리, 작업 재시도의 효과를 얻을 수 있다.

### SNS - MessageFiltering

![SNS-MessageFiltering](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUuN9H%2FbtrAdYOE0DC%2Fd5wZJxzWvaMwMy3SIFcN5K%2Fimg.png)

- [i] FanOut patternw중 유용한 기능은  SNS에서 메시지를 필터링 할 수 있다는 것이다!
	SNS Topic을 구독한 다른 대기열로 메시지를 전송하기 전에 JSON정책에 따라 메세지를 수정하여 보낼 수 있다.


---
[SNS + SQS:Fan Out](https://ssunw.tistory.com/entry/%EB%94%94%EC%BB%A4%ED%94%8C%EB%A7%81-%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-SNS-SQS-Fan-Out)
[여러 컨슈머가 동일 토픽에서 메시지를 읽을 때 사용하는 주요 패턴 - 로드 밸런싱, 팬 아웃](https://knight76.tistory.com/entry/%EC%97%AC%EB%9F%AC-%EC%BB%A8%EC%8A%88%EB%A8%B8%EA%B0%80-%EB%8F%99%EC%9D%BC-%ED%86%A0%ED%94%BD%EC%97%90%EC%84%9C-%EB%A9%94%EC%8B%9C%EC%A7%80%EB%A5%BC-%EC%9D%BD%EC%9D%84-%EB%95%8C-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%A3%BC%EC%9A%94-%ED%8C%A8%ED%84%B4-%EB%A1%9C%EB%93%9C-%EB%B0%B8%EB%9F%B0%EC%8B%B1-%ED%8C%AC-%EC%95%84%EC%9B%83)