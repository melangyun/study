레디스의 비트맵은 문자열 자료형의 비트를 작접 조작하여 사용한다.
비트맵은 비트로 구성된다.
- 비트(bit): 0,1로 구성, 레디스에서는 문자열의 각 비트를 개별적으로 조작할 수 있다.
- 오프셋(offset): 비트맵에서 비트 위치를 지정하는 인덱스. 0부터 시작
필요한 메모리는 비트 수에따라 결정되고, 1바이트(1byte)를 최소 단위로 계산

# 레디스 비트맵 명령어
```redis-cli
SESTBIT key offset value
```
특정 키의 비트맵에서 지정된 오프셋의 비트를 지정

```redis-cli
GETBIT key offset
```
특정 키의 비트맵에서 지정된 오프셋의 비트를 가져옴

```redis-cli
BITCOUNT key [start end]
```
비트맵에서 1로 설정된 비트의 수를계산

```redis-cli
BITOP operation destkey key [key...]
```
하나 이상의 비트맵에 대해 비트 연산을 수행하고 결과를 새 비트맵으로 저장

> 지원되는 연산 `AND`, `OR`, `XOR`, `NOT`

>[!example] 레디스 비트맵을 이용하여 사용자 활동을 추적하는게 가장 대표적인 활용 사례이다.

