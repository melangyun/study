![머클트리와 머클루트](https://steemitimages.com/1280x0/https://steemitimages.com/DQmSvecCtezcV2JhK8ounENdrqNptJdGcDCibdftoMDTPf4/tree_root.png)

1. 최초 데이터를 SHA256 형태의 해시값으로 변환한다.
2. 가장 가까운 노드 2개를 한쌍으로 묶어 합친 후 해시값으로 변환한다.
3. 계속해서 해시값으로 변환하여 마지막 하나가 남을 때 까지 이 과정을 반복한다.
블록의 바디정보에 저장된 트랜잭션의 정보들이 유효한지 빠르게 검사하기 위한 역할을 수행하는것이 `머클 루트`이다.

- 블록헤더의 머클루트 값은 블록바디의 거래내역 정보인 `TXID`의 해시트리 결과값이다.
- 머클루트의 역할은 각 거래정보의 TXID의 정보들이 변경되었는지에 대한 유효성을 검사하는 역할을 수행한다.
- 머클루트의 결과 값을 통해 블록 해시의 정보가 구성됨으로 그 블록의 유효성 또한 검사할 수 있다.


---
[머클 트리와 머클 루트 설명](https://academy.gopax.co.kr/meokeul-teuriwa-meokeul-ruteu-seolmyeong/)
[머클트리 및 머클루트에 관한 정의](https://steemit.com/kr/@yahweh87/4-merkle-tree-merkle-root)