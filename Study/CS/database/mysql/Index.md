[Index 그리고 Ascending, Descending Index](https://velog.io/@boo105/Index)
[기억보단 기록을;\[mysql\] 인덱스 정리 및 팁](https://jojoldu.tistory.com/243)

## Index 장단점

- [p] 장점
- 데이터들이 정렬되어있다
	> `WHERE`, `ORDER BY`, `MIN`, `MAX` 의 효율성이 높아진다.
- 테이블을 조회하는 속도와 그에 따른 성능을 향상시킬 수 있다.
- 전반적인 시스템의 부하를 줄일 수 있다.

- [c] 단점
- Index를 관리하기 위해 DB의 약 10%에 해당하는 저장공간이 필요하다.
- Index를 관리하기 위해 Index 관리 작업이 필요하다.
- Index를 잘못 사용할 경우 오히려 성능이 저하되는 역효과가 발생할 수 있다.
- Index는 테이블의 전체 데이터 중에서 <u>10~15% 이하의 데이터를 처리하는 경우에만 효율적</u>이고 그 이상의 데이터를 처리할 땐 Index를 사용하지 않는 것이 더 낫다.

## Index 관리
DBMS는 Index를 항상 최신으로 정렬 상태로 유지해야 원하는 값을 빠르게 탐색할 수 있다.
그렇기 때문에 Index가 적용된 데이터에 INSERT, UPDATE, DELETE가 수행된다면 각각 다음과 같은 Index 처리과정을 추가적으로 해주어야 한다.

- INSERT: 새로운 데이터에 대한 Index를 추가함
- DELETE: 삭제하는 데이터의 Index를 사용하지 않는다는 작업을 진행함
- UPDATE: 기존의 데이터에 해당하는 Index를 사용하지 않게 처리하고, 갱신된 데이터에 대해 Index를 추가함

> [!fail] index컬럼에 update, delete 시 index 테이블의 크기가 커진다.
> update, delete를 할 경우, index테이블에서 없에는 것이 아니라, 사용하지 않도록 하기 때문에, 너무 빈번한 발생을 한다면 문제가 될 수 있다.

>[!tip] index의 갯수는 3~4개 까지가 적당하다.
>- 너무 많은 인덱스는 새로운 Row를 등록할때마다 인덱스를 추가해야하고, 수정/삭제시마다 인덱스 수정이 필요하여 성능상 이슈가 있을 수 있다.
>  - 인덱스 역시 공간을 차지합니다. 많은 인덱스들은 그만큼 많은 공간을 차지한다.
>  - 특히 많은 인덱스들로 인해 **옵티마이저가 잘못된 인덱스를 선택할 확률이 높다**.

>[!question] 그래서 어디에 Index를 쓰는게 좋을까
>- 어느정도 규모가 있으며
>- `insert`, `update`, `delete`가 너무 빈번하지 않아야함
>- `join`, `where`, `order by`가 자주 사용되는 테이블
>- 테이블의 중복도가 낮은 테이블

### index의 크기
InnoDB (MySQL)은 디스크에 데이터를 저장하는 가장 기본 단위를 **페이지**라고 하며, **인덱스 역시 페이지 단위로 관리(16KB로 고정)** 된다.
(B-Tree 인덱스 구조에서 Root, Branch, Leaf 참고)

> 만약 본인이 설정한 인덱스 키의 크기가 16 Byte 라고 하고, 자식노드(Branch, Leaf)의 주소(위 인덱스 구조 그림 참고)가 담긴 크기가 12 Byte 정도로 잡으면, `16*1024 / (16+12) = 585`로 인해 하나의 페이지에는 585개가 저장될 수 있습니다. 여기서 인덱스 키가 32 Byte로 커지면 어떻게 될까요?   `16*1024 / (32+12) = 372`로 되어 372개만 한 페이지에 저장할 수 있게 됩니다. 

조회 결과로 500개의 row를 읽을때 16byte일때는 1개의 페이지에서 다 조회가 되지만, 32byte일때는 2개의 페이지를 읽어야 하므로 이는 성능 저하가 발행하게 됩니다.

> 인덱스의 키는 길면 길수록 성능상 이슈가 있습니다.
## Index 구조

### 1. B+ Tree(Balanced-Tree)
참고: [[B+Tree vs B-Tree]]
![B+Tree](https://velog.velcdn.com/images/boo105/post/cb2290e3-d1d5-4a13-b919-09f57c8db30f/image.png)
B+Tree는 DB의 Index를 위해 <u>자식 노드가 2개 이상인 B-Tree를 개선시킨 자료구조</u>이다.
구조는 위와 같이 Root, Branch, Leaf Node로 구성되며 계층적 구조를 갖고 있다.
B+Tree는 모든 노드에 데이터를 저장했던 B-Tree와 다르게 밑에와 같은 특성을 가지고 있다.

- Leaf Node만 Index와 함께 데이터를 가지고 있다.
- 나머지 노드인 Index Node들은 데이터를 위한 Index만을 갖는다.
- Leaf Node들은 LinkedList로 연결되어 있다.
- 데이터 노드 크기는 Index Node의 크기와 같지 않아도 된다.
- Leaf Node를 제외하고 데이터를 가지지 않기 때문에 메모리 공간의 확보로 더 많은 key들을 가질수 수 있다.
  > 따라서 노드당 많은 key를 보유할 수 있기 때문에 트리의 높이는 낮아지게 된다.
- Full Scan 시, B+tree는 Leaf Node에 데이터가 모두 있기 때문에 한 번의 선형탐색만 하면 되기 때문에 B-tree에 비해 빠르다.
	> (B-tree는 모든 노드 확인해야함.)

### Hash Table

Hash 테이블은 Key, Value로 데이터를 저장하는 자료구조 중 하나로 빠른 데이터 검색(`O(1)`)이 가능하다.  
Hash 테이블 기반의 DB Index는 `(데이터, 데이터의 위치) -> (Key, Value)`로 사용하여 컬럼의 값으로 생성된 Hash를 통해 Index를 구현한다.

> [!warning] 하지만 HashTable은 잘 사용되지 않는다.
> 이유는 Hash가 등호(=) 연산에만 특화되어 있고 부등호 연산(>, <)에 적합하지 않기 때문
> 부등호 연산이 자주 사용되는 DB는 HashTable이 적합하지 않다.

---
연관 링크 [[5. 조회 최적화를 위해 인덱스 이해하기#^533e28]]

## Ascending index vs Descending index

- Ascending index : 작은 값의 인덱스 키가 B-Tree의 왼쪽으로 정렬된 Index
- Descending index : 큰 값의 인덱스 키가 B-Tree의 왼쪽으로 정렬된 Index
---
- Forward Index Scan (Forward scan) : Index Leaf Node의 왼쪽 페이지부터 오른쪽으로 스캔 (왼쪽 -> 오른쪽)
- Backward Index Scan (Backward scan) : Index Leaf Node의 오른쪽 페이지부터 왼쪽으로 스캔 ( 오른쪽 -> 왼쪽)
> [!Note] index scan 방향에 따라 성능 차이도 존재한다.
InnoDB 스토리지 엔진에서는 페이지 잠금 과정에서 데드락을 방지하기 위해서 B-Tree의 왼쪽에서 오른쪽 순서(Forward)로만 잠금을 획득하도록 하고 있다.
그래서 Forward index scan에서는 다음 페이지 잠금 획득이 매우 간단하지만, Backward index scan에서 이전 페이지 잠금을 획득하는 과정은 상당히 복잡한 과정을 거치게 된다. 이런 차이로 인서 많은 페이지를 스캔해야 하는 Index scan에서는 잠금 획득으로 인한 쿼리 처리 지연이 발생하게 된다.
>> [!check] Backward Index Scan < Forward Index Scan


- [p] 따라서 최신의 데이터를 불러오는 쿼리가 잦다면 Descending index가 좋을것이다.