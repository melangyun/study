> Multi-Version Concurrency Control


MVCC를 이용하는 이유는 락을 사용하지 않기 위해서이다. [[동시성 제어]]를 위한 가장 쉬운 방법이 락이지만, 락을 사용하면 동시 요청 시에 처리 속도가 상당히 떨어진다. 따라서 MySQL은 MVCC를 사용하고 있으며, 스냅샷으로 언두 로그(Undo Log)를 활용한다.

**MVCC(Multi-Version Concurrency Control)** 는 동시 접근을 허용하는 데이터베이스에서 동시성을 제어하기 위해 사용하는 방법 중 하나이다.

- <u>MVCC에서 데이터에 접근하는 사용자는 접근한 시점에 데이터베이스의 Snapshot을 읽는다.</u>
- [!] snapshot 데이터에 대한 변경이 완료(commit)될 때 까지의 변경사항은 다른 데이터베이스 사용자가 볼 수 없다.

- 이후에 사용자가 업데이트하면 **이전의 데이터를 덮어 씌우는게 아니라 새로운 버전의 데이터를 UNDO 영역에 생성**한다. 대신 이전 버전의 데이터와 비교해서 변경된 내용을 기록한다.
	이렇게 해서 <u>하나의 데이터에 대해 여러 버전의 데이터가 존재하게 되고, 사용자는 마지막 버전의 데이터를 읽게 된다.</u> 

> [!tip] MVCC 의 특징
> - 일반적인 RDBMS보다 매우 빠르게 작동

MVCC의 접근 방식은 잠금을 필요로 하지 않기 때문에 일반적인 RDBMS보다 매우 빠르게 작동한다.
<u>또한 데이터를 읽기 시작할 때, 다른 사람이 그 데이터를 삭제하거나 수정하더라도 영향을 받지 않고 데이터를 사용할 수 있다.</u>

> [!warning] MVVC 주의점
> - 사용하지 않는 데이터가 계속 쌓이게 되므로 데이터를 정리하는 시스템이 필요하다.
> - MVCC 모델은 하나의 데이터에 대한 여러 버전의 데이터를 허용하기 때문에 데이터 버전이 충돌될 수 있으므로 애플리케이션 영역에서 이러한 문제를 해결해야 한다.
> - <u>또한 UNDO 블록 I/O, CR Copy 생성, CR 블록 캐싱 같은 부가적인 작업의 오버헤드 발생</u> 한다. 이러한 구조의 MVCC는 문장수준과 트랜잭션 수준의 읽기 일관성이 존재한다.

# MySQL에서 MVCC

MySQL의 InnoDB에서는 Undo Log를 활용해 MVCC 기능을 구현한다. 이해를 위해 실제 쿼리문 예시를 가지고 살펴보도록 하자. 

예를 들어 아래와 같은 CREATE 쿼리문이 실행되었다고 하자.

```sql
CREATE TABLE member (
    id INT NOT NULL,
    name VARCHAR(20) NOT NULL,
    area VARCHAR(100) NOT NULL,
    PRIMARY KEY(m_id),
    INDEX idx_area(area)
)

INSERT INTO member(id, name, area) VALUES (1, "MangKyu", "서울");
```

그러면 데이터는 다음의 상태로 저장이 된다.
![저장된 디비 구조](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6txYY%2FbtrRZN1BXuj%2F8iRkKk4RkjnxhKG8pwrUbk%2Fimg.png)
```SQL
UPDATE member SET area = "경기" WHERE id = 1;
```
![Update 문 실행 후](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcg8wmO%2FbtrSGWDIdL5%2FA8tBSFwPK9G6bPNxJeFtYK%2Fimg.png)
> 먼저 Commit 여부와는 상관 없이 InnoDB 버퍼 풀은 새로운 값으로 갱신된다.
> 그리고 Undo 로그에는 변경 전의 값이 복사된다.그리고 InnoDB 버퍼 풀의 내용은 백그라운드 쓰레드를 통해 디스크에 저장이 되는데, 반영 여부는 시점에 따라 다를 수 있다.

`Commit` 이나 `Rollbak` 이 호출되지 않은 상태에서 다른 사용자가 아래와 같은 쿼리로 조회하면 어떤 결과과 조회될까?

```SQL
SELECT * FROM member WHERE id = 1;
```

그 결과는 트랜잭션의 격리 수준(Isolation Level)에 따라 다르다. 만약 커밋되지 않은 내용도 조회하도록 해주는 READ_UNCOMMITTED라면 <u>버퍼 풀의 데이터를 읽어서 반환</u>하며, 이는 커밋 여부와 무관하게 변경된 데이터를 읽어 반환하는 것이다.

만약 READ_COMMITED 이나 그 이상의 격리 수준(REPEATABLE_READ, SERIALIZABLE)이라면 변경되기 이전의 <u>Undo 로그 영역의 데이터를 반환</u>하게 된다. 이것이 가능한 이유는 하나의 데이터에 대해 여러 버전을 관리하는 MVCC 덕분이다.

**여기서 Undo Log 영역의 데이터는 커밋 혹은 롤백을 호출하여 InnoDB 버퍼풀도 이전의 데이터로 복구되고, 더 이상 언두 영역을 필요로 하는 트랜잭션이 더는 없을 때 비로소 삭제된다.**
MVCC를 이용하는 이유는 락을 사용하지 않기 위해서이다. 동시성 제어를 위한 가장 쉬운 방법이 락이지만, 락을 사용하면 동시 요청 시에 처리 속도가 상당히 떨어진다. 따라서 MySQL은 MVCC를 사용하고 있으며, 스냅샷으로 언두 로그(Undo Log)를 활용한다.


#  잠금 없는 일관된 읽기(Consistent Non-Locking Read) 

MySQL은 MVCC를 통해 락 없이 읽기 작업을 수행할 수 있다. 그래서 *격리 수준이 SERIALIZABLE 만 아니라면* 순수한 읽기 작업은 다른 트랜잭션과 무관하게 항상 잠금 대기 없이 바로 실행된다.

<u>특정 사용자가 레코드를 변경하고 아직 커밋하지 않았더라도 데이터를 변경하는 트랜잭션이 다른 트랜잭션의 읽기 작업을 방해하지 않는다.</u> 이를 잠금 없는 일관된 읽기(Consistent Non-Locking Read)라고 표현하며, 앞서 살펴보았듯 이는 언두 로그를 통해 가능하다.


# 트랜잭션 범위 안의 읽기와 트랜잭션 범위 밖의 읽기

가끔 트랜잭션 내에서 실행되는 SELECT와 트랜잭션 없이 실행되는 SELECT의 차이를 혼동하는 경우가 있다. READ COMMITTED 수준에서는 트랜잭션 내에서 실행되는 SELECT와 트랜잭션 밖에서 실행되는 SELECT의 차이가 별로 없다. 하지만 REPEATABLE READ 격리 수준에서는 기본적으로 SELECT 문장도 트랜잭션 범위 내에서만 작동한다.

즉, START TRANSACTION (또는 BEGIN) 명령으로 트랜잭션을 시작한 상태에서 온종일 동일한 쿼리를 반복해서 실행해봐도 동일한 결과만 보게 된다. 아무리 다른 트랜잭션에서 그 데이터를 변경하고 COMMIT 해도 말이다. 별로 중요하지 않은 차이처럼 보이지만, 이런 문제로 데이터의 정합성이 깨지고 이로 인해 애플리케이션 버그가 발생하면 찾기가 쉽지 않다.



---
[MVCC(다중 버전 동시성 제어)와 언두 로그(Undo Log), 리두 로그(Redo Log)](https://mangkyu.tistory.com/288)
[[Database] MVCC(다중 버전 동시성 제어)란?](https://mangkyu.tistory.com/53)


