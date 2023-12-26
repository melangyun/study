클로저는 자바스크립트 고유 개념이 아니라, 함수를 일급 객체로 취급하는 함수형 프로그래밍 언어(FP; 얼랭(Erlnang), 스칼라, 하스켈, 리스프)에서 사용되는 중요한 특성이다.

클로저는 JS고유의 개념이 아니므로, ECMAScript 명세에 클로저의 정의가 등장하지 않는다.
클로저에 대해 MDN은 아래와 같이 정의한다

> [!cite] 클로저는 함수와 그 함수가 선언됐을 때의 렉시컬 스코프(Lexical scope) 사이의 관계를 나타내는 개념이다.
> 클로저는 반환된 내부함수가 자신이 선언되었을 때의 환경인 스코프를 기억하여 자신이 선언됐을 때 환경 밖에서 호출되어도 그 환경에 접근할 수 있는 함수를 말한다.
> > 자신이 생성될때의 환경(Lexical enviroment)을 기억하는 함수다.


```js
function outFunc(){
	var x = 10;
	var innerFunc = function () { 
		console.log(x); 
		// 내부함수 innerFunc는 자신을 포함하고 있는 외부함수 outFunc의 변수 x에 접근할수 있다
	};
	innerFunc();
}

outFunc();
```

스코프는 함수를 호출하는 시점이 아니라, <u>함수를 어디에 선언하였는지에 따라</u> 결정된다. 이를 **렉시컬 스코핑(Lexical scoping)** 라 한다.

클로저는 주로 다음과 같은 환경에서 활용된다.

1. 데이터 은닉(Data Encapsulation)
	클로저를 사용하여 변수를 은닉하고 함수를 통해서만 해당 변수에 접근 할 수 있도록 만들 수 있다
2. 콜백 함수(Callback Functions)
	비동기 작업에서 콜백 함수로 사용되어 외부 스코프의 변수에 접근할 수 있게 한다.
3. 모듈 패턴
	클로저를 활용하여 모듈처럼 동작하도록 함수와 변수를 그룹화할 수 있다

## 콜백함수와 클로저 예시

콜백 함수는 다른 함수에 인자로 전달하고, 이후에 해당 함수 내에서 비동기적으로 실행되거나 필요한 타이밍에 호출되는 함수이다.

```js
function fetchData(url, callback){
	// 비동기적으로 데이터를 가져오는 함수

	// ..

	// 데이터 가져오기가 완료되면 콜백 함수 호출
	const data = "Some data from the server";
	callback(data);
}

const processAndLogData = (function (){
	let counter = 0;
	return function(data){ // data 접근
		console.log("Data: ", data);
		counter++;
		console.log("counter: ", counter);
	}
})()
fetchData("https://example.com/api/dat", processAndLogData);
// Data: Some data from the server
// counter: 1
fetchData("https://example.com/api/dat", processAndLogData);
// Data: Some data from the server
// counter: 2



```

`processAndLogData`함수가 클로저로 감싸져 외부 스코프에 있는 `counter` 에 접근할 수 있다.
또한 data에 `processAndLogData` innterFunction에서 접근할 수 있다.

---
[Closure; 클로저](https://poiemaweb.com/js-closure)