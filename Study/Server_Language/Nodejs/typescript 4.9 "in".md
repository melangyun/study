typecasting없이 사용 할 수 있다
```ts
interface RGB {
  red: number;
  green: number;
  blue: number;
}

interface HSV {
  hue: number;
  saturation: number;
  value: number;
}

function setColor(color: RGB | HSV) {
  if ("hue" in color) {
  // 이제 'color'의 타입은 HSV 입니다.
  }
}
```
> 하지만 string으로 사용해서 생각보다 사용을 하지 않을수도..


```ts
if (type === 'requester') Participant is Requester
```


---
[typescript4.9 ReleaseNote](https://www.typescriptlang.org/ko/docs/handbook/release-notes/typescript-4-9.html#in-연산자를-사용하여-정의되지-않은-프로퍼티로-타입-좁히기)