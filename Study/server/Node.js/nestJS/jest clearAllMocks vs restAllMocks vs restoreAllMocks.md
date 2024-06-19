# 1. jest.clearAllMocks()
```ts
beforeEach(() => {
  jest.clearAllMocks();
});
```
Jest 가 생성한 모든 Mock함수의 호출 기록과 인스턴스 삭제.
Mock호출 기록을 초기화 할 때 유용.
- 장점: 모든 Mock함수의 호출 기록 초기화. 각 테스트가 독립적으로 실행 될 수 있다.
- 단점: Mock 함수 자체의 구현은 유지된다. Mock함수의 동작 자체는 변경되지 않는다.

# 2. jest.resetAllMocks()
```ts
beforeEach(() => {
  jest.resetAllMocks();
});
```
Jest가 생성한 모든 Mock함수의 호출 기록과 인스턴스 삭제. Mock함수의 기본 구현도 초기화
- 장점: Mock 함수의 호출 기록 뿐 아니라, 함수 자체의 구현도 초기화. 테스트 간 완전 격리 보장
- 단점: Mock함수 기본 구현 초기화

# 3. jest.restorAllMocks()
```ts
beforeEach(() => {
  jest.restoreAllMocks();
});
```
Jest가 생성한 모든 Mock 함수를 원래의 실제 구현으로 되돌림.
스파이(spy)한 메서드가 원래의 메서드로 복구된다.

- 장점: Mock 함수가 원래의 실제 함수로 돌아가기 때문에, 테스트 이후에 실제 함수의 동작을 확인할 수 있다.
- 단점: 모든 Mock이 원래의 구현으로 돌아가므로, 특정 Mock 상태를 유지해야 하는 경우에는 적합하지 않다


---
- jest.clearAllMocks(): 모든 Mock 함수의 호출 기록과 인스턴스를 지움. 함수의 구현은 유지.
- jest.resetAllMocks(): 모든 Mock 함수의 호출 기록과 인스턴스를 지우고 함수의 기본 구현을 초기화.
- jest.restoreAllMocks(): Mock 함수를 원래의 실제 구현으로 되돌림.
