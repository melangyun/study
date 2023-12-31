동시성 제어를 위한 기술 중 하나. (운영체제 알고리즘으로도 사용된다.)
CAS는 여러 스레드나 프로세스가 동일한 데이터를 동시에 업데이트하는 상황에서 발생하는 경쟁 조건을 방지하기 위한 메모리 연산이다.

기본적으로 두 단계로 이루어 진다.
1. 비교(Compare): 현재 메모리에 저장된 값과 예상되는 값이 일치하는지 확인한다.
2. 교체(Swap): 값이 일치하면 새로운 값으로 메모리를 교체한다.

이 과정에서 CAS는 다른 스레드가 값을 변경하지 않았는지 비교 후에 교체하므로, 경쟁 조건을 방지할 수 있다. (이는 Lock을 이용하는 전통적인 방법보다 성능적으로 우위이다.)

- [p] 경쟁 조건을 방지하면서 lock보다 성능이 좋을 수 있다.
- [c] 일부 상황에서 원자성을 보장하지 못할 수 있다.

> Java에서는 `java.util.concurrent.atomic`패키지에서 `AtomicXXX`클래스들이 CAS를 활용하여 스레드 안전한 연산을 제공한다.


- [!] 반복 시도에 따른 성능 손실을 고려해야한다. 또한 문제의 특성에 따라 적절한 방법을 선택하는 것이 중요하다.

