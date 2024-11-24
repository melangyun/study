# LFU(Least Frequently Used)
<u>가장 적게 사용된 데이터를 제거</u>하는 알고리즘.
- 최근에 추가된 데이터 불리
	새로운 데이터가 캐시에 추가되지마자 사용 빈도가 낮으면 금방 제거가 될 수 있다.
	최근 데이터는 충분한 사용 기회 없이 바로 삭제되는 이슈가 있음
- 사용 빈도 기록 비용
	사용 빈도를 계속해서 추적해야하기 때문에, 저장해야 할 메타데이터가 많아지면서 메모리 비용이 커질 수 있다.

# TinyLFU 동작 원리
TinyLFU는 LFU의 장점을 유지하면서도 메모리 사용량을 줄이고, 새로운 데이터를 캐시에서 제거하지 않고 충분한 기회를 줄 수 있도록 설계된 알고리즘
## 1. Probabilistic Counting(확률 카운팅)
모든 데이터를 *정확하게 추적하는 대신, **사용 빈도를 확률적으로 저장.***
이를 통해 메모리 사용량을 줄이고도 비슷한 성능을 유지할 수 있다. 이 때 **CountMin Sketch** 라는 데이터 구조를 사용해 사용 빈도를 압축해서 기록
- **CountMin Sketch**: 메모리 효율적으로 사용 빈도를 추적하기 위한 데이터 구조.
  오차가 존재해 실제 사용 빈도보다 더 많이 기록될 수 있지만, 성능을 위해서는 충분히 허용할 수 있는 수준
## 2. Windowed Admission
Windowed Admission이라는 기법을 통해 새로운 데이터가 충분히 기회를 갖도록 함. 즉, 최근 데이터가 무조건 제거되지 않고, 사용 빈도가 충분히 높아질 때까지 캐시에서 살아남을 기회 제공

**세가지 영역**으로 구성
- Window
	새로운 데이터가 처음 들어오는 영역. 최근 사용 여부를 먼저 체크함.
	일정 기간 동안 빈도가 높다면 캐시에 남고, 그렇지 않다면 제거된다.
- Main Cache
	사용 빈도가 높은 데이터가 저장. 사용 빈도가 높은 데이터는 오래 캐시에 남아있을 수 있음
- Probation
	아직 사용 빈도가 높지 않지만, Window를 통과한 데이터가 임시로 머무르는 공간.
	사용 빈도가 낮아지면 여기서 제거될 수 있다.

---
**Tiny LFU의 장점**
- 메모리 사용량 감소
- 새로운 데이터에 대한 공정성
- 효율적인 제거


> [!info] TinyLFU와 Caffeine
> TinyLFU는 Caffeine 캐시 라이브러리에서 기본적으로 사용되는 eviction알고리즘.
> 이 라이브러리가 높은 성능을 유지하는 중요한 이유중 하나가 TinyLFU를 사용하기 때문이다.
