HTTPS(Hypertext Transfer Protocol Secure)는 HTTP에  S 한 글자가 추가된것이다. HTTP에서 보안 (secure)이 강화된 프로토콜

HTTP의 보안은 `SSL(Secure Sockets Layer)` 에서 담당한다.
- 클라와 서버가 서로 데이터를 암호화해 통신할 수 있도록 돕는 보안 계층
![SSL](https://t1.daumcdn.net/brunch/service/user/5xeg/image/hwvnQeEGBq_aON8lfHeh4yzaznE.PNG)

> [!tip] OSI의 각 계층은 서로 독립되어 있기 때문에 SSL또한 HTTPS뿐만 아니라 다른 프로토콜과 조합해서 사용할 수 있다.

- TLS? SSL?
	`SSL2.0`에 몇가지 취약점이 발견되어, 이를 해결하기 위해 아예 구조를 재설계해 `SSL 3.0`을 배포함
	그 이후 기존 버전과 구분하기 위해 <u>3.0 다음부터 등장한 SSL의 이름을 `TLS`로 변경하였음.</u>
	>  다만 사람들이 SSL이란 이름에 더 익숙하다보니, SSL을 더이상 사용하고 있지 않아도 SSL로 불리우고 있음


# 공개키 기법과 대칭키 기법

SSL은 **공개키 기법**과 **대칭키 기법**이라는 두 암호화 기법을 함께 사용한다.

- 대칭키 암호화
	하나의 키로 암호화와 복호화를 둘 다 할 수 있는 암호화 기법
	- [p] 공개키 방식에 비해 암호화나 복호화에 속도가 빠르다
	- [c] 키를 안전하게 서로 교환하기 어렵다
		클라와 서버가 같은 키를 갖고있어야 하므로, 서로 키를 통신해야 하는데 키를 가로챌 위험이 있다.
- 공개키 암호화(Public Key Encryption) / 비대칭키 암호화 (Asymmetric Key Encryption)
	- 서로 다른 *키 두개(공개키, 개인키)로 암호화, 복호화를 한다*
		- 공개키로 암호화 -> 개인키로 복호화 가능
		- 개인 키로 암호화 -> 공개키로 복호화 가능
	- 공개키는 누구나 가질 수 있는 키지만, 개인키는 소유자 한 명만 가질 수 있다.

# SSL 동작 과정

- 핸드셰이크
- 세션
- 세션 종료

![SSL동작 과정](https://img1.daumcdn.net/thumb/R1280x0.fjpg/?fname=http://t1.daumcdn.net/brunch/service/user/5xeg/image/lT_WtjqhblcdCgCDMRiOW6Y46Xs.PNG)

1. Client Hello
	랜덤한 데이터와 현재 지원할 수 있는 암호화 방식을 서버에게 전달
	> 암호화 방식을 전달하는 이유는, 같은 대칭키 공개키 기법이라도 다양한 암호화 방식이 있으므로 서로 어떤 암호화 방식을 사용할지 협의하는 과정이 필요하기 때문이다.
	- TLS version
	- Cipher Sute list (Client가 지원하는 암호화 방식들; 서버와 클라이언트가 서로 지원하는 암호화 방식이 다를 수 있어 Handshake를 통해 어떤 암호화 방식을 사용할 것인지 정해야 한다.)
	- Client Random Data
		클라이언트에서 생성한 난수. 이후 대칭키를 만들 때 사용된다.
	- Session Id
		  매번 연결을 할때마다 Handshake를 하는것은 시간이 소요되므로, 최초 한번의 HandShake만 Full Handshake를 하기로 함
	  - SNI(Server Name Indication)
		  IP주소 하나에 여러개의 도메인이 연결되기 때문에 IP주소에 접속할 때 어떤 도메인에 접속하는지 명시하는 부분이 SNI
![Handshake](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbvtDjP%2FbtqGc9RBd7J%2Fd3xo4MlQGNeqzy7HveWYXk%2Fimg.png)
> SessionID를 활용함으로서 시간상 약 100ms정도 절약된다고 한다.

2. Server Hello
	클라이언트가 전달한 내용과 동일한 랜덤 데이터와 지원 가능한 암호화 방식, `인증서` 를 전달.
	- **인증서: CA**(Certificate Authority)에서 발급받은 문서
		서버가 신뢰할 수 있는지 보장하는 역할
	- **TLS Version**
	- **Selected Suite**
		Client가 보낸 암호화 방식 중 서버가 사용 가능한 암호화 방식을 선택하여 보냄
	- **Server Random Data**
		서버에서 생성한 난수. 클라이언트와 동일하게 대칭키를 만들 때 시용
	- **Session ID**
	- SNI(Server Name Indication) -> 비워보냄
3. Server Certificatie
	- 클라이언트는 서버 인증서를 확인하고, 이전에 주고 받았던 `클라이언트의 난수, 서버의 난수`를 조합하여 `pre master secret(대칭키)`이라는 키를 생성
4. Server Hello Done
	- 서버 -> 클라이언트 : 보낼 메시지를모두 보냈다 보내는 메시지
5. Client Key Exchange
	- `pre master secret`키를 <u>서버의 공개키로 암호화한것</u>을 서버에 보냄
6. Key Generation (통신 과정 x)
	- 클라이언트와 서버가 서로 암, 복호화 할 때 사용할 대칭키를 성공적으로 공유
7. Cipher Spec Exchange (Server & Client)
	- 이 이후로 전송되는 모든 메시지는 협상된 알고리즘과 키를 이용하여 암호화 하겠다는 메시지를 나눔
8. Finished (Server & Client)
	- Client와 Server가 TLS Handshake를 성공적으로 마치고 종료함

---
[그림으로 쉽게 보는 HTTPS, SSL, TLS](https://brunch.co.kr/@swimjiy/47)
[TLS(SSL) - 3. Handshake](https://babbab2.tistory.com/7)