
더티체킹은 주로 ORM(Object-Relational Mapping)에서 사용되며, 개발자가 DB작업을 조금 더 추상화하고 편리하게 다룰 수 있게 해준다. 예를들어 Hibernate에서는 영속 상태의 엔티티에서 변경이 감지되면 해당 엔티티를 `'더티'` 상태로 표시하고, 트랜잭션이 커밋될 때 변경사항을 데이터베이스에 반영한다.

- [p] 개발자가명시적으로 데이터 베이스 업데이트를 다루지 않아도 된다.
      코드를 간결하게 유지하고, 오류를 방지하는데 도움이 된다. 또한 더티 체킹은 트랜잭션을 통해 일관된 상태를 유지하므로, DB작업에 대한 안정성을 제공한다.
- 더티체킹은 주로 트랜잭션과 함께 사용된다.

---

```java
@Slf4j
@RequiredArgsConstructor
@Service
public class PayService {

    public void updateNative(Long id, String tradeNo) {
        EntityManager em = entityManagerFactory.createEntityManager();
        EntityTransaction tx = em.getTransaction();
        tx.begin(); //트랜잭션 시작
        Pay pay = em.find(Pay.class, id);
        pay.changeTradeNo(tradeNo); // 엔티티만 변경
        tx.commit(); //트랜잭션 커밋
    }
}
```
1. 트래잭션 시작
2. 엔티티 조회
3. 엔티티 값 변경
4. 트랜잭션 커밋
여기에서, `update`에 관련된 코드는 없다.

하지만 이를 동작시켜보면 update쿼리가 동작된다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class PayServiceTest {

    @Autowired
    PayRepository payRepository;

    @Autowired
    PayService payService;

    @After
    public void tearDown() throws Exception {
        payRepository.deleteAll();
    }

    @Test
    public void 엔티티매니저로_확인() {
        //given
        Pay pay = payRepository.save(new Pay("test1",  100));

        //when
        String updateTradeNo = "test2";
        payService.updateNative(pay.getId(), updateTradeNo);

        //then
        Pay saved = payRepository.findAll().get(0);
        assertThat(saved.getTradeNo()).isEqualTo(updateTradeNo);
    }
}
```

이유는 **`Dirtychecking`** 때문!
- Dirty: 상태의 변화가 생긴 정도!
- Dirty checking: 상태 변경 검사
>  JPA는 트랜잭션이 끝나는 시점에 <u>변화가 있는 모든 엔티티 객체</u>를 DB에 자동으로 반영해준다.
>
- [?] 변화가 있다의 기준 -> 최초 조회 상태

JPA에서는 엔티티를 조회하면 해당 엔티티의 조회 상태 그대로 스냅샷을 만들어 놓는다.
그리고 트랜잭션이 끝나는 시점에 이 스냅샷과 비교해서, 다른점이 있다면 Update Query를 데이터 베이스로 전달한다.

> [!tip] 당연히 상태 변경 검사 대상은 영속성 컨텍스트가 관리하는 엔티티이다.
> - detach된 엔티티(준영속)
> - DB에 반영되기 전 처음 생성된 엔티티(비영속)
> 
> 준영속/ 비영속 상태의 엔티티는 Dirty Checking 대상에 포함되지 않는다.
> 값을 변경해도 





---
기억보단 기록을: [더티 체킹 (Dirty Checking)이란?](https://jojoldu.tistory.com/415)