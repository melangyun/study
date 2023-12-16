
# 자바스크립트를 통해 **비동기**를 처리하는 방법
- call back funciton
	> - call back hell을 만든다.
- Promise
	> - 여러 promise를 디버깅하는데 힘들다
- async / await
	> - 에러핸들링 깔끔
	> - 콜백 지옥으로 부터 빠져나올 수 있다.
	
> [!tip] 유의해야 할 부분은, async await 는 Promise를 가독성 좋게 사용하는 한 가지 방법에 불과하다는 것이다.

# 여러개의 비동기 처리를 한번에 하고싶다면?

- [*] 순서가 보장되지 않아도 되는 상황에서, 비동기 작업을 일렬로 하고싶다면?

```js
async function awaitFunc(time){
    return new Promise(
    (resolved, rejected) => 
    setTimeout(()=> resolved("success"))
    )
}
// async await 을 사용하였을 경우
console.time("소요시간")
await awaitFunc(1000)
await awaitFunc(2000)
await awaitFunc(3000)
await awaitFunc(4000)
await awaitFunc(5000)
console.timeEnd("소요시간")
// 소요시간: 5.794921875 ms

console.time("소요시간")
await Promise.all([
    awaitFunc(1000),
    awaitFunc(2000),
    awaitFunc(3000),
    awaitFunc(4000),
    awaitFunc(5000),
])
console.timeEnd("소요시간")
// 소요시간: 0.489013671875 ms
```
![asyc-await vs promise.all](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1yV49%2FbtqGYpxYRYP%2FzuhA7oic2ZxkZVQpQCwKT1%2Fimg.png)
> async-await은 blocking, promise.all은 병렬로 시행

> [!tip] Promise.all의 장점
> 병렬로 처리하여 더 빠르게 처리할 수 있다. 실패시에도 어떤 함수에서(먼저 끝난 함수에서) 중간에 어떤 함수에서 에러가 났을 때에 그 실패를 즉시 반환한다.

>[!warning] 단, javascript에서 실제 병렬로 처리하는것은 아니다!
> [[NodeJS Event Loop파헤치기]]참고해보기



---
참고
[언제 Promise.all을 사용해야 될까?](https://code-masterjung.tistory.com/91)
[정말 Promise.all()은 병렬로 실행될까?](https://mugglim.tistory.com/12)

