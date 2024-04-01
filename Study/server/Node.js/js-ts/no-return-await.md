코드를 작성하다 보면 아래와 같은 상황이 생긴다.
```ts
// pseudocode
@Controller()
class exampleController {
  @Post()
  async public calledService():Promise<ResponseDto>{
    return this.service.method();
  }
}
```
service에서 호출한 method가 `Promise` 를 반환하는데 사실 이를 수신한 단에서 특별히 처리해줄 것이 없을 경우 `await`없이 바로 반환을 해주고 싶은 경우이다.

이렇게 사용할경우, 에러 발생시 `error Trace` 가 명확히 추적되지 않는다. 때문에, 가급적 `await`을 붙여서 사용하는것이 좋다.
> 사실 이전에도 여러번 마주했던 문제인데, 어느순간부터 왜 그렇게 사용했는지 잊고 습관적으로 사용하고 있었고, 새로운 팀원분들이 이유를 물었을때.. 이유도 잊고 그냥 그렇게 사용해 왔다는 것을 깨달았다.

```ts
// (2)
export async function returnWithoutAwait() {
  return throwAsync('without await'); // await가 없는 return
}

// (3)
async function throwAsync(msg) {
  await sleep(10);
  throw Error(msg);
}

// test.ts
it('returnWithoutAwait', async () => {
  // (1)
  await returnWithoutAwait().catch(console.log);
});
```

위 코드는 실행시 `returnWithoutAwait`가 전혀 추적되지 않는다.

![trace가 보이지 않음](https://blog.kakaocdn.net/dn/E6Yvh/btrW6pBoJY9/0dNGFpIVoIYapBpKQNWAk0/img.png)

단일 함수와 `Promise.all`어디에서든 `return await`가 없다면, 비동기 스택에서는 Trace대상이 되지 않는다. 함수가 `Promise`를 반환하지만, `await`하지 않는다면 누락된 Trace가 발생할 수 있다. 이럴 경우 함수 오류를 추적하는 것을 어렵게 만든다.

또한 `ESLint v8.46.0` 에서부터 deprecated되었으며,  유지하는것보다 제거하는것의 `await`속도가 더 느려질 수도있다.



---
[eslint: no-return-await](https://eslint.org/docs/latest/rules/no-return-await)
[기억보단 기록을: no-return-await 는 항상 정답일까](https://jojoldu.tistory.com/699)