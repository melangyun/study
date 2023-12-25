AWS Step Function은 [[AWS Lambda 질문]] 및 Amazon ECS의 워크플로우를 연결하여 Serverless 서비스의 설계를 명확하고 유연하게 만들어준다.

> 특히 많은 데이터들을 Lambda를 통해 처리할 때 Lambda의 제한 시간 <u>900초는 부족하다.</u>
> Lambda의 Invoke를 사용해서 분산 API를 구성할 수 있지만, 유지보수가 힘들어지고, Invoke의 Timeout도 고려해야 한다.


그럴 때 Step Function을 고려해 볼만하다.
- AWS Step Functions을 사용하면 Serverless의 가시성이 확보되어 서비스를 빠르게 빌드하고 업데이트 할 수 있다. 
- <u>Lambda Function들을 유기적으로 연결</u>하여 오류와 예외처리를 쉽게 할 수 있다.
- 각 단위 Function들의 결합으로 코드를 간결하게 개발할 수 있다.
- [*] Step Functions을 통해 Serverless 환경으로 거의 모든 로직을 구현할 수 있다.

## step Function 동작 방식
- [[상태머신(State Machine)]] 기반으로 동작한다.

### Task State

1. Activity
   활동 작업을 사용하면 워크플로의 단계를 다른 곳에서 실행되는 코드 배치에 연결할 수 있다.
   활동 작업자라고 하는 이 외부 코드 배치는 작업을 위해 Step Functions를 폴링하고 코드를 사용하여 작업을 <u>비동기식으로 완료하고 결과를 반환</u>한다.
   활동 작업은 사용자 개입(예: 사용자 계정 확인)이 필요한 비동기식 워크플로에서 일반적이다.
2. Service
	서비스 작업을 사용하면 <u>워크플로의 단계를 특정 AWS 서비스에 연결할 수 있다</u>
	 Step Functions는 다른 서비스에 요청을 보내고 작업이 완료될 때까지 기다린 후 워크플로의 다음 단계를 계속합니다. Lambda 함수 실행과 같은 자동화된 단계에 쉽게 사용할 수 있다.

## Step Function의 사용

- 서버리스 마이크로 서비스의 오케스트레이션
- 데이터 처리 파이프라인 구축
- 보안 사고 대응 정의 등

Amazon SNS 구성 요소과 여러 Lambda함수를 호출 할 수 있다.

## Step Functions의 장점

1. 마이크로서비스 기반 애플리케이션의 단순화된 오케스트레이션 (Simplified orchestration)
AWS Step Functions는 애플리케이션 워크플로의 여러 단계를 조정합니다. 워크플로가 실행될 때 Step Functions는 수행 중인 단계와 단계 간에 전달되는 데이터를 추적하여 네트워크 장애가 발생하는 경우 애플리케이션이 중단된 부분을 선택할 수 있도록 합니다.

2.  향상된 애플리케이션 탄력성 (application resilience)
Step Functions는 워크플로 단계, 오류 및 다시 시작을 관리하여 애플리케이션 작업이 예상대로 실행되도록 합니다. 이렇게 향상된 애플리케이션 탄력성을 통해 실패하는 사용자 요청이 줄어듭니다.

3. 통합 코드의 필요성 감소
Step Functions를 사용하면 엔지니어는 분산 애플리케이션 구성 요소 간의 관계를 정의하는 통합 코드를 작성하는 데 소요되는 시간을 줄일 수 있습니다. Step Functions는 지정된 비즈니스 로직을 기반으로 병렬 프로세스, 예외 처리, 재시도 및 시간 초과를 자동으로 조정합니다.

4. 별도의 워크플로우 및 비즈니스 로직
Step Functions는 애플리케이션 구현 방법을 정의하는 코드에서 비즈니스 로직을 분리합니다. 이러한 분리를 통해 팀은 신속하게 워크플로를 수정하고, 구성 요소를 독립적으로 확장하고, 여러 애플리케이션에 대한 워크플로 코드를 재사용할 수 있습니다.
무엇보다도 AWS Step Functions의 주요 이점은 애플리케이션 구성 요소를 수동으로 조정하고 함께 작동하는 방법을 수동으로 정의할 필요가 없다는 것입니다. 결과적으로 엔지니어는 워크플로 코드 작성에 소요되는 시간을 줄이고 더 높은 가치의 비즈니스 로직에 더 집중할 수 있습니다.

 
---
참고
[datadog step funciton Intro](https://www.datadoghq.com/knowledge-center/aws-step-functions/)
[AWS Step Functions Tutorial](https://foobar123.com/aws-step-functions-tutorial-76b9f5a7b9c8)
[AWS Step Functions 이해](https://blog.leedoing.com/184)
[Step 함수를 사용하여 Lambda 호출](https://docs.aws.amazon.com/ko_kr/step-functions/latest/dg/connect-lambda.html)