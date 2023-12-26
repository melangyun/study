> [!tip] 동기화(Synchronization)
> 작업들 사이에 실행 시기를 맞추는 것
> - 여러 쓰레드가 동일한 자원(데이터) 접근 및 수정시 동기화 이슈(쓰레드 결과에 영향을 줌)

# Mutual exclustion(상호 배재)

쓰레드는 프로세스의 모든 데이터를 접근할 수 있다. 따라서 여러 쓰레드가 변경하는 공유 변수에 대해 Exclusive Access가 필요하다.

- [f] 어느 한 쓰레드가 공유 변수를 갱신하는 동안 다른 쓰레드가 동시 접근하지 못하도록 막는다.
---
- 임계자원(critical resource): 동시에 수정하면 안되는 자원
- 임계영역(critical section): 동시에 실행하면 안되는 코드


```python
g_count=0 # 임계자원

def workFunciton:
	global g_count
	lock.acquire() # 임계영역
	for i in range(10000):
		g_count += 1
	lock.release()
	
```

# 뮤텍스 Mutex, 세마포어 Semaphore

`Critical section(임계구역)`에 대한 접근을 막기 위해 Locking 매커니즘이 필요하다.

## Mutex(binary semaphore)

(0또는 1의 값만 갖기 때문에) 임계구역에 하나의 스레드만 들어갈 수 있음
- 당연히 성능상 이슈가 있을 수 있으므로 세마포어를 둠

## Semaphore(세마포어)

공유자원의 개수를 나타내는 변수. 임계구역에 여러 스레드가 들어갈 수 있다.
counter를 두어 동시에 리소스에 접근할 수 있는 허용 가능한 스레드 수를 제어한다.

> [!info] 세마포어는 깃발이라는 뜻을 가지고 있다.
> 기차길에서 깃발 표식으로 파란색이 걸려있으면 지나가도 되고, 빨간색이 걸려있으면 기다렸다가 다른 기차가 지나가게끔 하는 용도로 사용하는 깃발
> ![세마포어 깃발](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3bea1db0-8669-484c-9489-c86f9985dfda%2FUntitled.png?table=block&id=0d64d686-9e78-48bf-b00f-c4e820cf64ef&spaceId=6f17c40e-8b35-441b-8c72-e335140f0143&width=2000&userId=6bbec50e-093d-4597-99fe-6b12d5b139c6&cache=v2)
> 겹치는 부분이 두 기차가 공유하는 임계자원이다.

### 세마포어는 전통적인 linux에 구현되어 있는 하나의 `함수`이다.

- P: 검사 (임계영역 진입시)
	S값이 1이상이면, 임계영역 진입 후 S값 1차감(S값이 0이면 대기)
- V: 증가 (임계영역에서 나갈때)
	S값을 1더하고, 임계영역을 나옴
- S: 세마포어 값
	초기값 만큼 여러 프로세스가 동시 임계영역 접근 가능한 수

```python
# Sudo Code
P(S): wait(S){ 
	  while S <= 0 : # 대기 
	  ... 
	  S--; # 다른 프로세스 접근 제한 
} 

V(S): signal(S){ 
	S++; # 다른 프로세스 접근 허용 
}
```

### 바쁜 대기(busy waiting)

`wait()`은 S가 0인 임계영역에 들어가기 위해 <u>반복문</u>을 수행한다.
엄밀히 말하면 프로세스가 멈추어 있는 것이 아니라, **Loop를 돌고 있는 것**이라, 성능상 좋지 못하다.

따라서 운영체제 기술로 Loop를 보완한다.
- S가 음수일 경우 바쁜 대기(busy waiting)대신 ==대기 큐==에 넣는다.
- C의 경우 `wakeup()`함수를 통해 대기큐에 있는 프로세스 재실행

- sem_open(): 세마포어를 생성 
- sem_wait(): 임계영역 접근 전, 세마포어를 잠그고, 세마포어가 잠겨있다면 풀리 때 까지 대기
- sem_post(): 공유자원에 대한 저근이 끝날을 때 세마포어 잠금을 해제한다.



---
[과거에 공부했던 내용 다시 보면서 정리함](https://melangyun.notion.site/Thread-06305742473a42f9b8f972fcec82e8e2)