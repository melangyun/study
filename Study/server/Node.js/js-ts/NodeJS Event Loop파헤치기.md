
<iframe width="560" height="315" src="https://www.youtube.com/embed/v67LloZ1ieI?si=ORLHRZx0UlsG13Hi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# NodeJS특징

1. Single Thread 기반
2. Event Driven 아키텍처
3. Non Blocking I/O 모델

>[!warning] 이벤트 큐에서 스택으로 올라가는 조건
>- Stack이 비어있을때만 올라감!
>-> 따라서, 스택이 계속 바쁘다면, 매우 느려진다. 안바쁘게 만드는게 좋음 (복잡한 연산x)

- [?] Single Thread 기반인데, 어떻게 Non Blocking I/O를 제공할수 있을까?
	> Event Loop를 추상화 하여 제공하는 libuv 라는 library에서 알 수 있다.

> [!tip] 들어가기 전 정리부터
> 1. NodeJS에서 JS의 실행은 Main Thread에 의해서만 수행되고, 1개의 call stack을 가진다.
> 2. call stack실행은 동기적 blocking이기 때문에 NodeJs에서는 이를 극복하기 위해 Single Thread와 궁합이 좋은 비동기 callback 프로그래밍 방식은 EventLoop를 추상화한 libuv library를 사용
> 3. libuv 내의 Event Loop는 Main Thread에 상주하여 자바스크립트 비동기 실행의 임무를 수행함
> 	- 요청의 특징에 따라 커널 비동기 함수 또는 libuv 내의 Thread Pool에 작업을 위임하며
> 	  callback을 실행하기 위해 Event Queue에 적재된 callback을 empty 상태의 call stack으로 이동시킨다.
> 4. Event Loop는 6개의 단계로 이루어져 있으며 각 단계별로 Event Queue를 소유한다.
> 	Event Loop는 각 단계를 순차적으로 순회하며 반복적으로 callback들을 처리한다.


# NodeJs의존성 구조
![NodeJs 구성도](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*HkWLGh9Kn8MdO6xJZKBKnw.png)

## V8

구글에 의해 개발된 자바스크립트 엔진
- heap memory 할당 
- call stack 실행
- garbage collector기능
- JS코드를 기계어로 해석하여 OS가 바로 실행할 수 있는 상태로 만들어주는 것이 주된 업무.
	따라서 NodeJs환경에서 자바스크립트로 File과 Network의 I/O를 할 수 있다.

## libuv

비동기 I/O를 지원하는 C언어 Library로 <u>윈도우, 리눅스 커널을 Wrapping하여 추상화한 구조</u>로 되어있다.
- 커널의 비동기 API로 지원할 수 없는 작업을 비동기화 하기 위한 별도의 *Thread Pool*을 가짐
- Event Loop, Evnt Queue를 관리

>[!tip] stack 호출 > V8, 비동기 I/O EventLoop는 libuv가 담당

- [?] libuv가 Thread Pool을 가지고 있다면 NodeJS는 Single Thread 기반이 맞을까?

```js
setInterval(() => console.log('hi'), 1000)
while(true){}
// 결과는 어떻게 될까? -> 아무것도 찍히지 않는다!
```
> 무한루프의 blocking으로 인해 setInterval의 callback이 실행되지 못함
> **같은 실행 컨텍스트 안에 있기 때문이다.**

즉, JS 실행은 Main Thread에 의해서만 진행된다.

# Main Thread == Event Loop

- [c] ~~JS실행용 Main Thread 1개 + Event Loop를 위한 Thread 1개 => 총 2개~~
- [p] Event Loop는 Main Thread안에서 실행되며, callback 작업이 수행될 수 있도록 도와준다.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*A29uBxiS_ZtjfnyHHUD98g.png)
> Libuv안에 Event Loop + Event Queue + Thread Pool이 존재한다!
> - memory heap: 변수들이 저장되어있다.
> - stack에 코드들이 쌓여있다

각각의 요소들을 통해 어떻게 비동기 callback을 수행하는가
1. 요청이 들어오면 Event Loop가 해당 요청이 Blocking I/O인지 아닌지 판별한다.
2. 커널의 비동기 I/O의 지원을 받을 수 있는 Non-Blocking I/O요청일 경우
	- 커널의 interface로 해당 요청을 처리
	- Event Queue 에 callback을 등록함
3. Blocking I/O라면
	- (예를 들면 File/ Network작업들) libuv 내의 별도의 Thread Pool에서 Worker Thread를 선택하여 작업을 위임.
	- Worker Thread는 작업을 완료한 후 Event Queue로 callback을 등록
4. Event Loop는 **주기적으로 call stack이 비어있는지 체크**하고 Event Queue에 실행 대기중인 callback이 있다면 callback들을 call stack으로 이동시켜 Main Thread에 의해 실행될 수 있게 만들어준다.

![libuv](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*RUJ9zOQtfP1dHhLEUAODnw.jpeg)

즉, Event Loop는
- 요청을 특성에 맞게 커널이나 Thread Pool에 위임
- 실행 대기중인 callback을 Event Queue에 모았다가
- <u>Main Thread에 의해 실행될 수 있도록 call stack으로 옮기는 역할</u>을 한다.

# Event Loop Phases

- [c] ~~Event Loop는 모든 callback을 하나의 Event Queue에 담아서 관리~~

![6단계의 Event Loop](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*3-zl41t9nlC26sitsaNIuA.png)

> - Timer
> - Pending callbacks
> - idle, prepare
>  - Poll
> - Check
> - Close callbacks

총 6단계로 진행된다.
>[!tip] 모든 단계마다 Event queue를 소유하고 있다.
> Event loop는 각 단계를 돌며 해당 단계의 Event Queue에서 실행할 call stack으로 이동시킨다.


## 1. Timer
Timer단계는 Event Loop의 시작단계이다.
setInterval, setTimeeout과 같은 타이머에 관련된 callback을 처리한다.
> 타이머들이 호출되자마자 Event Queue에 들어가는 것이 아니고 내부적으로 min-heap 형태로 타이머를 구성하고 있다가 발동 단계가 되면 그때 Event Queue로 callback을 이동시킨다.

## 2. Pending Callbacks
pending queue에 들어있는 call back들을 실행한다.
pending_queue에는 이전 루프에서 완료된 callback(예를들면 Network I/O가 끝나고 응답받은 경우) 또는 Error callback등이 쌓이게 된다.

## 3.  Idle, Prepare
Idle에 함축된 뜻과는 다르게 Event Loop가 매번 순회할 때마다 실행되며 4번째 단계인 Poll을 위한 준비 작업을 하는 단계

## 4. Poll
대기중인 callback을 call stack으로 가장 많이 올려보내는 단계로 이 단계에서는 새로운 수신 커넥션을 위한 소켓과 데이터를 설정한다. Poll단계에서는 watch_queue를 바라보며 작업을 수행하는데 만약 Queue가 비어있지 않다면 배정받은 시간동안 Queue가 소진될때 까지 모든 callback을 call stack으로 올려 실행시킨다.

## 5. Check

Check 단계는 setImmediate() 만을 위한 단계입니다. 이 단계에서는 setImmediate를 사용하여 수행한 callback만 Event Queue에 쌓이고 call stack으로 올라갑니다.

## 6. Close Callbacks
Close 단계는 아래와 같은 close type의 callback을 관리하는 단계입니다.
```Js
socket.on('close', () => {})
```


---
<직방> [NodeJS Event Loop파헤치기](https://medium.com/zigbang/nodejs-event-loop%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0-16e9290f2b30)
[코딩애플-개발자 90%가 모르는 자바스크립트 동작원리 (Stack, Queue, event loop)](https://www.youtube.com/watch?v=v67LloZ1ieI)