> [!info] HTTP(HyperText Transfer Protocol) 프로토콜이란?
> W3 상에서 정보를 주고받을 수 있는 프로토콜
> 주로 HTML문서를 주고받는 데에 쓰인다. 주로 TCP를 사용하고, HTTP3부터는 UDP를 사용하며, `80`번 포트를 사용한다.

# HTTP 동작 방식

![HTTP 동작 방식](https://velog.velcdn.com/images%2Fgjrjr4545%2Fpost%2F29fe3754-ec09-4981-9fed-d15e3efbb910%2Fhttp-full-structure.png)

HTTP는 서버 사이에서 이루어지는 요청/ 응답 프로토콜이다.

> [!hint] 특징
> - Reqeust / Response
> 	한 컴퓨터에서 데이터 요청을 보내면 다른 컴퓨터에서는 그 요청에 따른 응답을 보내는 형식
> - 상태가 없는 Stateless프로토콜
> - Connetionless

# HTTP 발전

## HTTP 0.9

본래 HTTP초기버전에는 번호가 없었으나, 차후 버전과 구별하기 위해 `0.9` 로 불림
- 요청: 요청 방법 + 해당 경로
- Method: Get
- 응답 직후 종료
- HTTP Header가 없으며, HyterText이외에 다른 파일을 전송하지 않음
- 상태 / 오류코드 / 버전 없음

### 0.9 예시
- request:
```TEXT
 GET /user.html
```
- response:
```HTML
<HTML>
	Simple Page
</HTML>
```

## HTTP 1.0 - 확장

- 1996년 등장
- HTTP 버전 정보가 각 요청 사이내로 전송 가능
- `상태 코드`도 응답의 시작부분에 붙음
- `헤더` 개념 등작
	- 메타데이터 전송 허용 (프로토콜의 유연성 / 확장 가능성을 높임)
	- 평이한 HTML이외에 다른 문서들 또한 전송이 가능해짐 (`Content-Type`)
- 요청에 따른 결과에 대한 동작 (로컬 캐시) 기능
- Method: Get, HEAD, POST

- [c] 단순한 동작이 반복되면서 통신부하 발생

### 1.0 예시

- request
```TEXT
GET /myPage.html
HTTP/1.0
User-Agent: NCSA_Mosaic/2.0(Windows3.1)
```
- response
```TEXT
HTTP/1.0 200 OK
Content-Type:text/html
Content-Length: 137582
Expires: Thu, 01 Dec 1997 16:00:00 GMT
Last-Modified: Wed, 1 May 1996 12:45:26 GMT  
Server: Apache 0.84
```
- response resource:
```html
<HTML> 
	A page with an image 
	<IMG SRC="/myimage.gif">
</HTML>
```

## HTTP 1.1 - 표준 프로토콜

- 1997년 1월 등장
- Connection 재사용이 가능하여 `Keep-alive`가 가능
	![keep-alive 및 pipelining](https://velog.velcdn.com/images%2Fgjrjr4545%2Fpost%2F866e8643-f75f-4cae-b7b2-140c70058513%2Fimage.png)
	기존엔 프로세스를 처리하면 Connectionless특성으로 인해 Connection이 close된다.
	그에 따라서 요청/응답을 다시 요청해야 하는데, 요청/응답을 하기 전 클라이언트와 서버간의 연결을 위한 작업이 필요했다. 그에 따라 데이터를 주고 받는 시간이외에 나머지 추가인증 시간이 누적되어 Network Latency가 증가했다. 이를 개선하기 위해 Keep-alive개념이 도입, Connection을 유지해 인증 시간에 따른 레이턴시를 감소시킨다.
- `pipelining`의 등장으로 `Multi Request`가 처리 가능
	*첫번째 요청에 대한 응답이 완전히 전송되기 전에 두번째 요청을 가능하게 함*
	하지만 완전한 멀티 플랙싱이 아닌, <u>응답 처리를 미루는 방식</u>으로, 앞선 응답이 오지 않을경우 HOL Bloking발생
- Proxy Server 기능 추가, 간접 접근 지역
	- 같은 프로토콜을 사용하는 둘 이상의 어플리케이션 연결
	- 보안 개선
	- 성능 개선/ 비용절약
	- 트래픽 개선 및 사용자 접근 차단 기능
- Caching
- 단일 IP로 Multiple Web Site 사용 가능
	- 지원 소모를 줄임

### 1.1의 문제

- HOL(Head Of Line) Bloking: 특정 응답의 지연
	순차적으로 데이터를 요청하고 응답받는 작업 중, 먼저 받은 요청이 끝나지 않으면, 뒤에 요청이 아무리 빨리 끝나도 대기해야 하는 현상
- RTT(Round Trip Time)의 증가
	요청별로 connection 을 만들게되고, TCP상에서 동작하는 HTTP의 특성상 3-way Handshake가 반복적으로 일어나고, 또한 불필요한 RTT증가와 네트워크 지연을 초래하여 성능을 저하
- 무거운 Header 구조
	- header에 너무 많은 메타데이터 저장
	- 매 요청시 중복된 Header값을 전송하게 되며, 또한 domain에 설정된 Cookie정보도 매 요청시마다 Header에 포함
	- 이로 인해 전송하려는 데이터보다 헤더 값이 큰 경우 발생


## HTTP 2.0의 등장

- SDPY(구글 제안 프로토콜) 기반으로, 2015년 등장
- Binary Framework
	기존 plane text기반이 아닌, binary 프레임으로 구성
	파싱이 더 빠르며, 오류 발생 가능성이 낮음
- Frame: HTTP 2.0에서 통신의 최소단위
	최소의 하나의 프레임 헤더, 바이너리와 인코딩 작업
	![Frame](https://velog.velcdn.com/images%2Fgjrjr4545%2Fpost%2Fdbc21847-b3be-4b90-9df1-2276407d7342%2Fbinary_framing_layer01.svg)
- Message
	- 다수의 프레임
	- 요청/응답의 단위
	![Message](https://velog.velcdn.com/images%2Fgjrjr4545%2Fpost%2F0f6bd6f1-2e55-423e-bb12-f47357b1a7dd%2Fimage.png)
- Streams
	구성된 연결 내에서 전달되는 바이트의 양방향 흐름
	하나 이상의 메시지가 전달 가능하다.
	![streams](https://velog.velcdn.com/images%2Fgjrjr4545%2Fpost%2Fcf49f967-f55d-4add-8630-c3dc173a186b%2Fimage.png)
	

### 개선점

- Stream Prioritization
	리소스간의 우선순위를 설정하여 랜더링이 늦어질때 발생할수 있는 문제를 해결한다.
- Multiplexing 개선
	하나의 TCP connection내에서 다수의 Stream 생성
	하나의 요청이 지연되면, 나머지 응답이 늦어지는 Pipelining과 달리, request/response를 독립적으로 처리
	- 다수의 request/response를 동시에 처리 가능
	![Multiplexing 개선](https://velog.velcdn.com/images%2Fgjrjr4545%2Fpost%2F338149a8-b2e6-4842-a693-b873aa3476d7%2Fhttp1.0vshttp1.1vshttp2.0.PNG)
- Header Compression
	- 반복적으로 사용되는 헤더를 헤더 테이블 내의 인덱스로 표기
	- 헤더크기를 약 80% 줄임
- Server Push
	- 클라이언트가 요청하지 않아도, 필요가 예상되는 리소스를 서버가 미리전송
	- HTTP 1.1에서는 클라이언트가 HTML문서를 요청했고, 해당 HTML에 여러개의 리소스가 있는 경우 해석하면서 필요한 리소스를 재요청하는 방식인 반면, HTTP/2에서는 Server Push기법을 통해 클라이언트가 요청하지 않아도 리소스를 push해주는 방식

### 한계

2.0또한 TCP통신을 이용하기 때문에 1.1에 문제점에서 발생했던 문제들이 여전히 발생한다.
- 3-way Hanshake문제
- HOL(Head Of Line) Bloking

## HTTP 3.0

2019년도 등장
- TCP에서 UDP통신 방식인 QUIC(구글의 UDP기반 프로토콜)으로 바뀜

연결 설정시 레이턴시 감소
- 3-Way HandShake과정 생략
- 서버에 신호를 한번 주고 서버가 거기에 따른 응답만 하면 바로 통신 가능
흐름 속도의 개선

클라이언트 IP가 변경되어도 연결이 유지됨 (Connection ID)를 사용하여 서버와 연결 생성

---
[HTTP 프로토콜 발전](https://velog.io/@gjrjr4545/HTTP-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C-%EB%B0%9C%EC%A0%84)