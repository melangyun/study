# 개요

## 헤더 분류
- General 헤더: 메시지 전체에 적용되는 정보
- Request 헤더: 요청 정보
	- user-Agent ..
- Response헤더: 응답 정보
	- Server:Apache
- Entity헤더: 엔티티 바디 정도
	- Contenty-type:text/html
	- Contenty-Length:..
## HTTP Body

- [c] 폐기됨! 
message body-RFC2616(199년 과거)
> - 메시지 본문(message body)는 엔티티 본문(entity body)를 전달하는데 사용
> - 엔티티 본문은 요청이나 응답에서 전달할 실제 데이터
> - 엔티티 헤더는 엔티티 본문의 데이터를 해석할 수 있는 정보 제공
	- 데이터 유형(html, json), 데이터 길이, 압축 정보 등등

2014년 RFC7230~7235등장

> - 엔티티(Entity) -> 표현(Representation)
> - Representation = representation Metadata + Representation Data
> - 표현 = 표현 메타데이터 + 표현 데이터

- 메시지 본문(message body = payload)를 통해 표현 데이터 전달
- `표현`은 요청이나 응답에서 전달할 실제 데이터
- 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공
	- 데이터 유형(html, json), 데이터 길이, 압출 정보 등등
- 참고: 표현 헤더는 표현 메타데이터와 페이로드 메시지를 구분해야 하지만 생략함

# 표현

표현 헤더는 전송, 응답 모두 사용한다.

- Content-Type: 표현 데이터의 형식
- Content-Encoding: 표현 데이터의 압축 방식
- Content-Language: 표현 데이터의 자연 언어
- Content-Lenth: 표현 데이터의 길이

## Content-Type
표현 데이터의 형식 설명(미디어 타입, 문자 인코딩)
- text/html; charset-utf-8
- application/json
- image/png

## Content-Enconding
표현 데이터 인코딩
- 표현 데이터를 압축하기 위해 사용
- 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
- 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
ex) `gzip`, `deflate`, `identity` (identity:압축 x)


## Content-Language
표현 데이터의 자연 언어 표현
- 예
	- ko
	- en
	- en-US

## Content-Length

- `바이트` 단위
- Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨

# 콘텐츠 협상
클라이언트가 선호하는 표현 요청
- [!] 협상 헤더는 요청시에만 사용한다.

- Accept: 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클라이언트가 선호하는 자연언어

## 협상과 우선순위 (Quality Values)

```PLAIN TEXT
GET /event
Accept-Language: ko-KR;q=0.9;en-US;q=0.8,en;q=0.7
```

- Quality Values(q)값 사용
- 0~1, 클수록 높은 우선순위
- 생략하면 1
- Accept-Language: ko-KR,ko;q=0.9;en-US;q=0.8,en;q=0.7
	1. ko-KR;q=1 (q생략)
	2. ko;q=0.9
	3. en-US;q=0.8
	4. en;q=0.7


### 구체적인게 우선된다.

- Accept: text/\*, text/plain, text/plain;format=flowed, \*/\*
	1. text/plain;format=flowed
	2. text/plain
	3. text/\*
	4. \*/\*

### 구체적인 것을 기준으로 미디어 타입을 맞춴다.

- Accept: Text/\*; q=0.3, text/html;q=0/7, text/html;level=1, text/html;level=2; q=0.4, \*/\*;q=0.5


# 전송 방식

- 단순 전송
	- Content-Length에 대한 길이를 알 수 있을 때
- 압축 전송
	- `Content-Encoding` 를 추가로 넣어주어야 함
- 분할 전송
	- `Trnsfer-Encoding: chunked`
	- `Content-Length`를 보낼 수 없다.
	- 분할해서 전송하면 오는대로 보여줄 수 있다.
- 범위 전송
	- REQUEST
		- GET Range:bytes=1001~2000
	- RESPONSE 
		- Content-Range: bytes 1001~2000 / 2000

# 일반 정보

- From: 유저 에이전트의 이메일 정보
	- 일반적으로 잘 사용되지 않음
	- 검색 엔진 같은 곳에서 주로 사용 (요청에서 사용)
- Referer: 이전 웹 페이지 주소
	- 현재 요청된 페이지의 이전 웹 페이지 주소
		- A-> B로 이동하는 경우 B를 요청할 때 Referer:A 를 포함해서 요청
		- Referer를 사용해서 **유입 경로 분석 가능**
		- 요청에서 사용
- User-Agent: 유저 에이전트 애플리케이션 정보
	- 클라이어트의 애플리케이션 정보(웹 브라우저 정보, 등등)
	- 통계 정보
	- 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
	- 요청에서 사용
- Server: 요청을 처리하는 오리진(Origin) 서버의 소프트웨어 정보
	- proxy 서버가 아닌 origin server의 소프트웨어 정보
	- 응답에서 사용
- Date: 메시지가 생성된 날짜
	- 응답에서 사용


# 특별한 정보

- Host: 요청한 호스트 정보(도메인)
	- 요청에서 사용하며 필수이다
	- 하나의 서버가 여러 도메인을 처리해야 할 때
	- 하나의 IP 주소에 여러 도메인이 적용되어 있을 때
- Location: 페이지 리다이렉션
	- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면 Location 자동이동
	- 혹은 201 Created
- Allow: 허용 가능한 HTTP method
	- 405(Method Not Allowed)에서 응답에 포함해야 함
	- ex) `Allow: GET, HEAD, PUT`
	- 사실은 많이 사용하지는 않는다.
- Retry-After: 유저 에이전트가 다음 요청을 하기까기 기다려야 하는 시간
	- 503(Service Unabaliable): 서비스가 언제까지 불능인지 알려줄 수 있음

# 인증

- Authorization: 클라이언트 인증 정보를 서버에 전달
	- `Basic xxxxx`
	- 인증하는 여러가지 메커니즘이 있다. 거기에 따라 value가 완전히 달라진다.
- WWW-Authenticate: 리소스 접근시 필요한 인증 방법 정의
	- 리소스 접근시 필요한 인증 방법 정의
	- 401 Unauthorized 응답과 함께 사용
	- WWW-Authenticate: Newauth realm="apps", type=1, title="Login to \"apps\"", Basic realm="simple"


# 쿠키

- set-cookie: 서버에서 클라이언트로 쿠키 전달(응답)
- Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달

쿠키를 미사용 할 경우 모든 요청과 링크에 사용자 정보를 포함해야 한다.
- 모든 요청에 사용자 정보가 포함되도록 개발해야함
- 브라우저를 완전히 종료하고 다시 열면?

쿠키는 모든 요청에 쿠키 정보를 자동 포함한다. -> 보안에 유의해야한다.

- 사용처
	- 사용자 로그인 세션 관리
	- 광고 정보 트래킹
- 쿠키 정보는 항상 서버에 전송된다.
	- 네트워크 트래픽 추가 유발
	- 최소한의 정보만 사용(세션 id, 인증 토큰)
	- 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장  하고 싶으면 웹 스토리지(localStorage, sessionStorge) 참고
- [!] 보안에 민감한 데이터는 저장하면 안된다!(주민번호, 신용카드 번호 등 )

모든 요청에 쿠키 정보 자동 포함

## 쿠키 - 생명주기(Expires, max-age)

`Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT`
- 만료일이 되면 쿠키를 삭제한다.

`Set-Cookie:max-age=3600` (3600)초
- 0이나 음수를 지정하면 쿠키 삭제

- 세션 쿠키: 만료 날짜를 *생략하면* 브라우저 종료시 까지만 유지
- 영속 쿠키: 만료 날짜를 *입력하면 해당 날짜까지 유지*

## 쿠키 - 도메인

- domain=example.org
- 명시: 명시한 문서 기준 도메인 + 서브 도메인 포함
	- domain=example.org를 지정해서 쿠키 생성
		- example.org는 물론이고
		- dev.example.org도 쿠키 접근
- 생략: 현재 문서 기준 도메인만 적용
	- example.org에서 쿠키를 생성하고 <u>domain 지정을 생략</u>
		- example.org 에서만 쿠키 접근
		- dev.example.org는 **쿠키 미접근**


## 쿠키 - 경로

- path=/home
- 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
- 일반적으로 path=/ 루트로 지정
	- ex) path=/home
	- [p] /home
	- [p] /home/level1
	- [p] /home/level2
	- [c] /hello : `불가능`

## 쿠키 - 보안

- [i] secure, httpOnly, samesite

- secure
	- 쿠키는 http, https를 구분하지 않고 전송
	- secure를 적용하면 https인 경우만 전송
- httpOnly
	- xss 공격 방지
	- 자바스크립트에서 접근 불가(document.cookie)
	- HTTP 전송에만 사용
- SameSite
	- XSRF 공격 방지
	- 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송
