

![[데이저 블록형태로 쪼개어 저장.png]]
DBMS는 디스크에 데이터를 저장할 때 블록 형태로 쪼개어 디스크에 쓰게 된다. 하지만 commit을 할때 바로 디스크 데이터에 반영하지 않는다. (Disk io가 많아지는 것이므로)

대부분의 DB는 메모리나 Sequential한 log에 적어 이를 보관하고, 어느정도 데이터가 차게 되면 Block으로 만들어 하드디스크게 쓰게 된다.
> randaom access 보다 Sequential access가 더 빠르다
> [[Sequential access VS Random access]]

- [*] 바로 Data Block을 만들지 않는다.

## DB에 트랜잭션 발생시
DBMS는 이를 모두 Sequential한 Log형태로 보관한다.
> Sequential Log가 빠르므로. 특별한 연산이나 리소스 소모가 적고, 디스크 헤더의 움직임이 적어짐
![[WAL.png]]

Log가 적정 사이즈가 되면 이 데이터를 Data Block으로 만들어 DB에 Disk Write하게 된다.
이때 DB앞의 Log가 WAL(Write-Ahead Logging; 선행 기입 로그)이다.

트랜젝션을 로그에 일단 기입해 기록을 남기고, 데이터가 쌓이면 이를 Flush해 DB의 disk에 Data Block형태로 wirte하게 된다.

일단 Log에 적히게 되면 누가 조회를 해도 같은 데이터를 보여주는 일관성을 보장하게 되고, 서버가 다운돼도 이미 로그에 기입되었기 때문에 원자성을 보장할 수가 있음

---
[데이터베이스의 무결성을 모장해주는 WAL](https://bourbonkk.tistory.com/86)
