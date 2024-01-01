# URI(Uniform Resource Identifier)

리소스를 식별하는 통합된 방법

![uri](https://velog.velcdn.com/images/hi_nahyun/post/d00c43ba-d4a7-465f-9bfb-28bcf251ef4c/image.png)
- URI
	- 리소스를 식별한다(주민번호 처럼, 자원 자체를 식별)
	- Uniform: 리소스 식별하는 통일된 방식
	- Resource: 자원, URI로 식별할수 있는 모든것(제한 없음)
	- Identifier: 다른 항목과 구분하는데 필요한 정보
- URL
	- Resouce Locator (리소스 위치 포함)
	- 리소스가 있는 위치를 지정
- URN
	- Resouces Name(리소스 이름)
	- 리소스에 이름을 부여


![url, urn](https://velog.velcdn.com/images/bienlee/post/b802eb0a-b6df-46e6-b70a-d0ecfd575f1b/image.png)
> [!tip] 위치는 변할 수 있지만, 이름은 변하지 않는다.
> urn이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않았다.

## URL 전체 문법

```PLAINTEXT
- scheme://[userinfo@]host[:port][/path][?query][#fragment]
- https://www.google.com:443/search?q=hello&hl=ko
```

- 주로 프로토콜 사용
- 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
	- ex) http, https, ftp 등등
- http는 80포트, https는 443포트를 주로 사용, 포트는 생략 가능
- https는 http에 보안 추가 (HTTP Secure)

- userinfo: 잘 사용하지 않음
- port: 일반적으로 생략, 생략시 http는 `80`, https는 `443`
- path: 리소스 경로, 계층적 구조
- query
	- `key=value` 형태
	- `?` 로 시작, `&`로 추가 가능
	- `query param`, `query string` 으로 불림


# 웹 브라우저 요청 흐름

![http 메시지 전송](https://velog.velcdn.com/images/bienlee/post/d4067322-0193-47e9-a847-d12f9ef7e4bb/image.png)

전송 데이터: 웹 브라우저가 만든 HTTP 메시지

![전송 데이터](https://velog.velcdn.com/images/bienlee/post/b6cba73e-ea9f-4d57-94cc-86ce62d21830/image.png)

