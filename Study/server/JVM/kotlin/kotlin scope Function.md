![scopeFunction 정리](https://img1.daumcdn.net/thumb/R1280x0.fpng/?fname=http://t1.daumcdn.net/brunch/service/user/1OLd/image/hvIh5c47ZsceVhFAPw4VvfzluKw.png)

스코프 함수는 내부에서 제공하는 스코프를 객체인 this로 사용할 것인지, 아니면 매개변수인 it을 사용할 것인지가 중요하다. 그리고 반환값이 함수 결과인지를 잘 이해해야 한다.
> 스코프 함수는 코드를 더 간결하게 만들 수 있지만, 지나치게 사용할 경우 가독성이 떨어지고, 오류를 유발할 수 있다.


- `this` vs `it`
    - `this`: `run`, `with`, `apply`
    - `it`: `let`, `also`
    
- 반환값 처리
    - apply: this 반환
    - also: it반환
    - let, run, with: 람다 결과식 반환
    


# let

- context object: `it`
- return: lambda result

let 함수는 null safety call에 자주 쓰인다
제한 범위의 함수를 도입해서 코드 가독성을 높일 수 있다.


```kotlin
val length = str?.let { 
    println("let() called on $it")        
    processNonNullString(it)      // OK: 'it' is not null inside '?.let { }'
    it.length
}
```


# with

- context object: `this`
- return: lambda result

- [!] 확장 함수가 아니다. 
- 반환된 결과를 사용할 필요가 없는 경우, *콘텍스트 객체에서 함수를 호출*하는 데 사용하는 것이 좋다.
- 코드에서 `이 개체를 활용하여 다음을 수행한다.`로 읽음

```kotlin
val numbers = mutableListOf("one", "two", "three")
with(numbers) {
    println("'with' is called with argument $this")
    println("It contains $size elements")
}

val firstAndLast = with(numbers) {
    "The first element is ${first()}," +
    " the last element is ${last()}"
}
println(firstAndLast)
```


# run

- context object: `this`
- return: lambda result

- run은 `확장함수`와 `일반 함수(비 확장 함수; non-extension funciton)`로 호출할 수 있다.
- 확장함수의 경우 `run`은 `with`와 동일한 역할을 수행한다.

```kotlin
val service = MultiportService("https://example.kotlinlang.org", 80)

val result = servce.run {
    port = 8080
    query(prepareRequest() + " to port $port")
}

// the same code written with let() function:
val letResult = service.let {
    it.port = 8080
    it.query(it.prepareRequest() + " to port ${it.port}")
```

비 확장함수의 경우 _콘텍스트 객체가 없지만_, <u>여전히 람다 결과를 반환한다.</u>
비확장함수로 사용하면 표현식이 필요한 여러 문의 블록을 사용할 수 있다.

```kotlin
val hexNumberRegex = run {
    val digits = "0-9"
    val hexDigits = "A-Fa-f"
    val sign = "+-"

    Regex("[$sign]?[$digits$hexDigits]+")
}

for (match in hexNumberRegex.findAll("+123 -FFFF !%*& 88 XYZ")) {
    println(match.value)
}
```

# apply

- context object: `this`
- return: 객체 자신

- 콘텍스트 자체를 반환하므로 값을 반환하지 않고, 주로 수신자 객체의 멤버에 대한 코드를 작성하는 데 사용하는 것이 좋다.
	> 객체 구성시 주로 사용한다.
- 코드로 `객체에 다음 할당을 적용한다`로 읽을 수 있다.

```kotlin
val adam = Person("Adam").apply {
    age = 32
    city = "London"        
}
println(adam)
```

# also

- context object: it
- return: 객체 자신

- 콘텍스트 개체를 인수로 사용하는 작업을 할 때 유용하다.
- 해당 속성 함수 및 개체에 대한 참조가 필요한 작업에 사용하거나, _외부 범위에서 참조를 숨기고 싶지 않을 때 사용한다. (외부의 this)_
- 코드로 `그리고 객체로 다음도 수행한다`로 읽을 수 있다.

```kotlin
val numbers = mutableListOf("one", "two", "three")
numbers
    .also { println("The list elements before adding new one: $it") }
    .add("four")
    
// The list elements before adding new one: [one, two, three]
```
