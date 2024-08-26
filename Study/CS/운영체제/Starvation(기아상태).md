특정 프로세스의 우선순위가 낮아서 원하는 자원을 계속 할당받지 못하는 상태.

Starvation이 발생하는 스케줄링
- SJF(Shortest Job First)
	극단적으로 CPU 사용이 짧은 JOB을 선호하기 때문에 사용시간이 긴 프로세스는 CPU를 할당 받을 수 없다.
- SRT(Shortest Remaining time First)
	새로운 프로세스가 도달할 때마다 남은 burst time 보다 더 짧은 CPU burst time 이 있따면 선점하기때문에 긴 burst time을 가진 프로세스는 할당받을 수 없다.
- 우선순위 스케줄링
	우선순위가 낮다면 할당받기 어렵다.
	- SNP, feed back

## Starvation 문제 해결 방법
- **Aging(노화 기법)** 
	시간이 지남에 따라 우선순위가 낮은 작업의 우선순위를 점진적으로 높여준다.
	이를 통해 일정 시간이 지나면 낮은 우선순위의 작업도 결국 자원을 할당받아 실행 될 수 있다.
- 우선 순위가 아닌 요청 순서대로 처리하는 FIFO를 사용한다.
- 프로세스의 우선순위를 조정한다.

