`서버 리스폰스`나, `클라이언트 코드`에 따라 브라우저에 저장되는 작은 단위의 문자열 파일들

> 서버가 reponse로 set-cookie header로 붙여서 보내준다.
> 이 response를 클라이언트에 보내주고, 자동으로 cookie가 저장된다.
> 이 후 브라우저가 request를 보낼 때 cookie라는 헤더에 붙어서 전달된다.

쿠키는 유저 인증 뿐만 아니라, 브라우저 이용자에 대한 개인화된 기능과 데이터 제공 수단으로 사용할 수 있다.

## Set-cookie
`Set-cooke` HTTP 응답 헤더는 `서버`에서 사용자 에이전트로 쿠키를 보내는데 사용된다.
사용자 에이전트는 나중에 서버로 다시 보낼 수 있다.
- 여러 쿠키를 보내려면 동일한 응답으로 여러 `set-Cookie`헤더를 보내야 한다.

> `<cookie-name> = <cookie-value>` : 쿠키 이름과 해당 값을 정의한다. 쿠키 정의는 이름-값 쌍으로 시작된다.


## option 톺아보기
### Secure

서버에서 리스폰스를 보낼 때 이 설정을 추가해 주면 HTTPS를 사용할 때만 클라이언트에서 서버로 쿠키가 보내진다.

```plain-text
Set-Cookie: cookie_name=cookie_value; Secure;
```

### HttpOnly

이 설정을 추가하면 클라이언트가 자바스크립트 코드로 해당 쿠키에 접근할 수 없게 된다.
악의적으로 클라이언트가 개인정보에 직접 접근하는 것을 막을 수 있다.

```plain-text
Set-Cookie: cookie_name=cookie_value; Secure; HttpOnly;
```

### SameSite

Cross site request forgery (CSRF; XSRF)공격을 예방할 수 있는 설정

> [!question] CSRF
> 




---
[mdn;set-cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)