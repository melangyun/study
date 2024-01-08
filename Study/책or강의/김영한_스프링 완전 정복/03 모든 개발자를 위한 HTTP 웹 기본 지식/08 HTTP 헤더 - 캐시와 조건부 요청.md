# 캐시 기본 동작

## 캐시가 없을 때

같은 요청이 반복되어도 서버에서 계속해서 다시 응답을 만들어 보내준다.

- 데이터가 변경되지 않아도 계속 네트워크를 통해서 데이터를 다운받아야 한다.
- 인터넷 네트워크는 매우 느리고 비싸다.
- 브라우저 로딩 속도가 느리다.
- 느린 사용자 경험

## 캐시 적용

서버에서 캐시를 설정

- `cache-control: maxage=60` : 캐시가 유효한 시간 **(초)**
- 응답 결과를 캐시에 저장
- 다음 요청시에는 캐시를 이용하여 네트워크 요청을 보내지 않는다.

> - 캐시 덕분에 캐시 시간동안 네트워크를 사용하지 않아도 된다.
> - 비싼 네트워크 사용량을 줄일 수 있다.
> - 브라우저 로딩 속도가 매우 빨라진다.
> - 빠른 사용자 경험

- 캐시 시간 초과시 서버를 통해 데이터를 다시 조회하고 캐시를 갱신한다.
	(이 때 다시 네트워크 다운로드 발생)

> [!question] 하지만, 응답에 여전히 변화가 없더라도 다시 조회 및 갱신이 필요할까?
> 

# 검증 헤더와 조건부 요청

캐시 유효시간이 초과해서 서버에 다시 요청하면 두 가지 상황이 나타난다.
1. 서버에서 기존 데이터를 변경함
2. 서버에서 기존 데이터를 변경하지 않음

## 캐시 시간 초과

- <u>캐시 만료후에도 서버에서 데이터를 변경하지 않음</u>
- 데이터를 전송하는 대신에 저장해두었던 캐시를 재사용 할 수 있다.
- 단 클라이언트의 데이터와 서버의 데이터가 같다는 사실을 확인할 수 있는 방법이 필요하다.

```PLAIN TEXT
Last-Modified: 2024년 11월 10일 10:00:00
```

![응답 결과를 캐시에 저장](https://velog.velcdn.com/images/power0080/post/185370a1-05a9-4401-9073-5156919022c7/image.PNG)

- 요청을 다시 보낼때 이 정보를 넣어 보낸다.
  (캐시의 데이터 최종 수정일 전송: `if-modified-sinceㄷ`)

```PLAIN TEXT
# 캐시가 가지고 있는, 데이터 최종 수정일을 전송
REQUEST
if-modified-since: 2024년 11월 10일 10:00:00
```

- 서버에서 데이터가 아직 수정되지 않았다고 확인되면 아래와 같이 응답한다. (Body가 없다)
```PLAIN TEXT
RESPONSE
HTTP/1.1 304 Not Modified
Content-Type: image/jpeg
cache-control: max-age=60
Last-Modified: 2024년 11월 10일 10:00:00
```
- [f] 이 때 HTTP Body가 없다.

- 이제 이 결과를 다시 세팅하고 60초간 요청을 보내지 않는다.

### 정리

- 캐시 유효시간이 초과해도, 서버의 데이터가 갱신되지 않으면 
  `304 Not Modified + 헤더 메타 정보` 만 응답하며 `body`는 존재하지 않는다.
- 클라이언트는 서버가 보낸 응답 헤더 정보로 캐시의 메타 정보를 갱신한다.
- 클라이언트는 캐시에 저장되어 있는 데이터를 재활용한다.
- 결과적으로 네트워크 다운로드가 발생하지만 용량이 적은 헤더 정보만 다운로드 한다.


# 검증 헤더와 조건부 요청

- 검증 헤더
	- 캐시 데이터와 서버 데이터가 같은지 검증하는 데이터
	- `Last-Modified`, `ETag`
- 조건부 요청 헤더
	- 검증 헤더로 조건에 따른 분기
	- `if-Modified-Since:Last-Modified`사용
	- `if-None-Math: ETag`사용
	- 조건이 만족하면 200OK
	- 조건이 만족하지 않으면 304 Not Modified
- `if-Modifed-Since` 이후에 데이터가 수정되었으면?
	- 데이터 미변경시
		- `304 Not Modified`, 헤더 데이터만 전송
	- 데이터 변경 예시
		- `200 OK`, 모든 데이터 전송(Body 포함)
		- [u] 전송 용량

## Last-Modified, if-Modified-Since 단점

- 1초 미만(0.x 초) 단위로 캐시 조정이 불가능
- 날짜 기반의 로직 사용
- 데이터를 수정해서 날짜가 다르지만, 같은 데이터를 수정해서 데이터 결과가 똑같은 경우
- 서버에서 별도의 캐시 로직을 관리하고 싶은 경우
	- ex) 스페이스나 주석처럼 크게 영향이 없는 반경에서 캐시를 유지하고 싶은 경우

## 이태그! - ETag, If-None-Match

- [f] <u>캐시 제어 로직을 서버에서 완전히 관리하고, 클라이언트는 캐시 메커니즘을 모르게 된다.</u>

- ETag(Entity Tag)
- 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠
	- ETag: "v1.0", ETag: "a2jid"
- 데이터가 변경되면 이 이름을 바꾸어서 변경함(Hash를 다시 생성)
	- 예) ETag: "aaaa" -> "bbbb"
	> 파일 라이브러리를 사용하면 파일이 같으면 같은 해시값이 나온다.
- 단순하게 `ETag` 만 보내서 같으면 유지, 다르면 다시 받기

# 캐시와 조건부 요청 헤더

## 캐시 제어 헤더

- Cache-Control: 캐시 제어
- Pragma: 캐시 제어(하위 호환)
- Expires: 캐시 유효 기간(하위 호환)


### Cache-Control

- max-age: 캐시 유효기간, 초단위
- no-cache: 데이터는 캐시해도 되지만, `항상 원(origin) 서버에 검증하고 사용`
- Cache-Control: no-store
	- 데이터에 민감한 정보가 있으므로 저장하면 안됨
	  > (메모리에서 사용하고 최대한 빨리 삭제)
	  
### Pragma; 캐시 제어(하위호환)

- Pragma: no-cache
- HTTP 1.0 하위 호환 `-> 지금은 사용하지 않음`

### Expires; 캐시 만료일 지정(하위호환)

- 캐시 만료일을 정확한 <u>날짜로 지정</u>
- HTTP 1.0 부터 사용
- 지금은 더 유연한 Cache-Control: max-age 권장
- Cache-Control: `max-age`와 함께 사용하면 Expires는 무시

### 검증 헤더와 조건부 요청 헤더

- 검증 헤더(Validator)
	- ETag
	- Last-Modified
- 조건부 요청 헤더
	- `if-Match`, `if-None-Match`: ETag값 사용
	- `if-Modified-Since`, `if-Unmodifeid-Since` : Last-Modified값 사용

# 프록시 캐시

- CDN 서비스

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdrWxcp%2FbtrUws1O2Co%2FJtz7oxu0MNqTYktotlK7p1%2Fimg.png)

> local 저장 캐시는 privae, 프록시 캐시 서버는 public
## Cache-Control

캐시 지시어(directives) - 기타

- Cache-Control: public
	응답이 public 캐시에 저장되어도 됨
- Cache-Control: private
	응답이 해당 사용자만을 위한것임. private 캐시에 저장해야 함(기본값)
- Cache-Control:s-maxage
	프록시 캐시에만 적용되는 max-age
- Age: 60(HTTP)
	오리진 서버에서 응답 후 프록시 캐시 내에 머문 시간(초)

# 캐시 무효화

## 확실한 캐시 무효화 응답

정말 캐시가 되면 안되는 요청에는 아래 설정들을 다 넣어주면 된다.

- Cache-Control: `no-cache`, `no-store`, `must-revalidate`
- Pragma: `no-cache`
	- HTTP 1.0 하위 호환

### 캐시 지시어(directives) - 확실한 캐시 무효화

- Cache-Control: `no-cache`
	데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용
- Cache-Control: `no-store`
	데이터에 민감한 정보가 있으므로 저장하면 안됨
- Cache-Control: `must-revalidate`
	- 캐시 만료 후 최초 조회시 원 서버에 검증해야함
	- 원 서버 접근 실패시 반드시 오류가 발생해야 함 - 504 (Gateway Timeout)
	- `must-revalidate` 는 캐시 유효 시간이 유효하다면 캐시를 사용함
- Pragma: `no-cache`
	- HTTP 1.0 하위 호환

### no-cache vs must-revalidate
![](https://velog.velcdn.com/images/tngh4037/post/7d2f7f36-23f3-4dc8-8220-a27a326d2d0d/image.png)

no-cache 기본 동작: 만일 원 서버에 확인할 수 없다면, 장애가 나는것보다는 그래도 오래된 데이터라도 보여준다.
must-revalidate: 원서버 접근 실패시 실패



