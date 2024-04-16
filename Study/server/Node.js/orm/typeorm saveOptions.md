- `data`
	- persist 메서드로 전달한 추가 데이터.
- `listeners`
	- `listeners`과 `subscribers`가 호출되는지 여부를 나타낸다. (hook)
	- 기본적으로 활성화 되어있다.
- `trnasaction`
- `chunk`
	- 큰 삽입을 수행하는 경우 수행 필요
- `reload`
	- 저장 이후 엔티티를 다시 로드해야하는지 여부
	- `returning/outpu`문을 지원하지 않는 DB에서만 동작. 기본적으로 켜져있음

---
[typeorm공식문서](https://orkhan.gitbook.io/typeorm/docs/repository-api#additional-options)