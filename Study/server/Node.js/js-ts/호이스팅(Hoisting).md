인터프리터가 코드를 실행하기 전 함수, 변수, 클래스, 또는 임포트의 선언문을 해당 범위의 맨 위로 <u>끌어 올려지는 것 처럼 보이는</u> 현상을 나타낸다.

1. 변수 선언 전 변수 값을 사용할 수 있는 경우 (`value hoisting`)
	- `function`
	- `function*`
	- `async function`
	- `async function*`
	- `import`
2. 변수 선언 전 해당 범위의 변수를 참조할 수 있지만 `ReferenceError`를 던지지 않고 값이 `undefined`인 경우 (`Declaration hoisting`)
	- `var`
3. 변수를 선언시 변수가 선언 이전 범위에서 동작이 변경됨
	- `let`
	- `const`
	- `class`
4. 변수 선언을 포함된 나머지 코드를 평가하기 전 변수의 사이드 이팩트 발생
	- `import`

## 간혹 let, const, class 는 호이스팅이 일어나지 않는다고 알려져 있는데, 이는 옳지 않다.

```javascript
const x = 1;
{
	console.log(x); // Uncaught ReferenceError: Cannot access 'x' before initialization
	const x = 2;
}
```

`const x = 2`선언이 호이스팅 되지 않는다면 `x = 1`값을 읽을 수 있어야 한다.
하지만 `const`선언은 여전히 정의된 전체 범위를 오염시키기 때문에, `console.log(x);`는 아직 초기화되지 않은 지역변수 `const x = 2`선언에서 `x`를 대신 읽고 `ReferenceError`를 던진다.

> [!tip] var, let, const
> var는 `전역 / 함수 범위` 이며 `let과 const는 블록범위`이다.


---
[mdn:호이스팅](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)