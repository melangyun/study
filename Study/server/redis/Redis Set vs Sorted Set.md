# Redis Set
해시테이블로 구현되어있다. (모든 연산이 상수시간에 수행)
- 삽입 (`SADD`): O(1)
- 삭제(`SREM`): O(1)
- 멤버 존재 여부 검사 (`SISMEMBER`): O(1)
- 전체 멤버 수 조회 (`SCARD`): O(1)
- 전체 멤버 조회(`SMEMBERS`): O(N)

# Redis Sorted Set
<mark style="background: #D2B3FFA6;">Skip List</mark>와 <mark style="background: #D2B3FFA6;">해시테이블</mark>의 조합으로 구현되어있다.
- 삽입(`ZADD`): O(logN)
- 삭제(`ZREM`): O(logN)
- 업데이트(`ZINCRBY`): O(logN)
- 순위 조회(`ZRANK`): O(logN)
- 범위 조회(`ZRANGE`): O(logN + M), 여기서 M은 반환되는 요소의 수
- 전체 멤버 수 조회(`ZCARD`): O(1)
- 특정 점수 범위의 멤버 수 조회(`ZOUNT`): O(logN)


- [!] 공간복잡도
	- Set: 각 요소에 대해 해시 테이블의 오버헤드가 추가된다. 평균적으로 요소당 일정한 크기의 메모리를 차지
	- SortedSet: 각 요소에 대해 Skip List와 해시 테이블의 오버헤드가 추가됨

