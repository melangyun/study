[코틀린 인터뷰 질문 (번역)](https://myung6024.tistory.com/286)

> [!question] Kotlin에서 val과 var의 차이점은 무엇입니까?

Kotlin에서 val은 Java의 final 키워드와 동일하다.
값이 지정되면 변경할 수 없으며 변경할 수 없습니다. var는 일반 변수처럼 변경 가능하다.

> [!question] 아래 문장이 문법적으로 맞을까요?

```kotlin
var number // line 1
number = 10 //line 2
```


---
 컴파일 타임 오류가 발생한다.
 Kotlin은 **컴파일 타임에 타입 유추를 사용**한다.
 따라서 위의 코드 라인은 변수 "number"가 명시적으로 언급하지 않았기에 컴파일러가 어떤 타입의 숫자인지 확인할 수 없어 오류가 발생한다.

> [!question] 다음 프로그램의 결과값을 알려주세요

```kotlin
var employee1 = Employee("maria", 1)
var employee2 = Employee("john", 2)
var employee3 = Employee("peter", 3)
var employee4 = Employee("peter", 3)
println(employee1 == employee2) 
println(employee3 == employee4)
println(employee1.equals(employee2))
println(employee3.equals(employee4))  
}

class Employee(var name: String, var id: Int) {
override fun equals(obj: Any?): Boolean {
   if (obj is Employee) {
	   return name == obj.name && id == obj.id
   }
   return false
}
}
```
---
`false, true, false, true`
`==` 및 `.equals`는 Kotlin에서 동일하다.
Java와 달리 둘 다 구조적 동등성(equal)를 확인한다.

> [!question] Kotlin에서 주소값이 동일한 것을 어떻게 확인할 수 있을까요?

`===` 삼중 등호 연산자를 사용합니다.

> [!question] Kotlin에서 Unit과 Nothing의 차이점은 무엇인가요?

1. **Unit**
	Java의 void와 동일하다.
	함수가 유용한 것을 반환하지 않거나 리턴해줄 값이 아무것도 없으면 암시적으로 Unit을 반환한다.
2. **Nothing**
	함수가 여기에서 반환되지 않고 예외가 발생하거나 무한 루프에 들어갈 것이다.
	Nothing함수를 호출한 후에는 컴파일러에서 연결할 수 없다고 인지하게 된다.

> [!question] Kotlin에서 싱글톤 클래스를 어떻게 생성합니까?

```kotlin
object classname { }
```

```java
// 빌드 결과
public final class classname {
   @NotNull
   public static final classname INSTANCE;
	private classname() {}
	static {
	      classname var0 = new classname();
	      INSTANCE = var0;
	   }
}
```
>
**"object"** 라는 키워드를 사용하여 생성할 수 있다.

> [!question]  companion object와 object의 차이

 [[object and companion object (kotlin)]]
==object는 싱글톤 패턴과 익명객체로 사용할 수 있다.==
companion object 는 클래스 내부에 선언할 수 있는 object인데 java의 static method와 동일히 사용할 수 있다.
> 클래스 자체로 function선언 가능 혹은 private property에 접근할수 있기 때문에 factory 패턴으로 사용하기도 적합하다.

> [!question] 다음 코드는 컴파일이 가능할까요?

```kotlin
class Bird(name: String) {
 fun capitalizeBirdName(){
        name.replaceFirstChar { it.uppercase() }
    }
}
```
---
name은 생성자의 paramter이기 때문에 접근할 수 없다.
다음과 같이 코드 수정을 할 수 있을것이다.

```kotlin
class Bird(var name:String){
	fun capitalizeBirdName(){
		name.replaceFirstChar {it.upperCase()}
	}
}
```
property는 일반 paramter과는 다르다.
- 기본 setter, getter가 있다.
- 클래스 내 어디에서나 엑세스 할 수 있다.
- 데이터를 저장할 필드가 있다.

>[!question] 코틀린에서 기본 데이터 타입?

코틀린의 자료형은 참조형 자료형을 사용한다.
자바에서는 int, long, float 등 기본형과 참조형을 함께 사용하지만, 코틀린은 모두 참조형 자료형을 사용한다.

[Kotlin 면접 질문 #01](https://brunch.co.kr/@oemilk/215)

> [!question] kotlin의 타겟 플랫폼은? kotlin-java간 상호 운용성은 어떻게 되는가

JVM(Java Virtual Machine)이 kotlin의 타겟 플랫폼이다.
Kotlin은 컴파일 시 바이트 코드를 생성하므로, Java와 100% 상호 운용이 가능하다.
따라서 Java에서 Kotlin코드를 호출 할 수 있으며, 그 반대의 경우도 마찬가지 이다.
	
> [!question] Null safety와 Nullable Type이란? Elvis 연산자란?

Kotlin은 Null Pointer Exception을 방지하기 위해 nullable타입을 이용하고, 이러한 타입들은 null 값을 가질 수 있다.
Elvis 연산자는 이런 nullable 타입들을 안전하게 이용하도록 사용할 수 있다. `?:` 의 형태

```kotlin
var str:String? = "뚠뚠"
var newStr = str?: "Default Value"

str = null
newStr = str?: "개미는"
```

> [!question] const와 val의 다른점은?

기본적으로 val properties는 runtime에 설정된다.
하지만 `const`를 사용하게 되면, val는 compile-tile 상수가 된다. 
- [!] 또 const는 var와 지역변수에 사용할 수 없다.

>[!question] `!!`와 `?`의 차이점은? nullable 값을 안전하게 이용할 수 있는 다른 방법은?

`!!`는 nullable타입의 값을 강제로 확잔하기 위해 사용된다.
- 만약 값이 `null` 이면, 런타임 에러가 발생한다. 
- [!] 따라서 null값이 아니라고 확신할 때만 이용해야 한다.

`?` 는 안전하게 nullable타입의 값을 가져올 수 있는 Elvis연산자 이다.
`let`을 이용해서 안전하게 nullable 타입의 값을 가져올 수 있다.
```kotlin
var str:String? = "뚠뚠"
str?.let {println(str)}

str = null
str?.let {println(str)} // DO NOTING
```

> [!question] `==`와 `===`의 차이점은?

- `==`: value비교
- `===`: reference 비교

>[!question] 아래 상속 구조는 컴파일이 되는가?
>```kotlin
> class A {}
> class B: A(){}
> ```

안된다. `open`을 붙여야 한다.

>[!question] Kotlin에서 생성자 타입들은?

- Primary
	- class header에 정의
	- logic을 가질 수 없다.
	- class 당 하나만 있다.
- Secondary
	- class body에 정의한다.
	- primiary 생성자가 있는 경우, 반드시 deltegate해야 한다.
	- logic을 가질 수 있다.
	- class 당 1개이상 있을 수 있다.

```kotlin
class User(name:String, isAdmin:Boolean){ // primary constructor

	// secondary constructor
	constructor(name:String, isAdmin:Boolean, age:Int): this(name, isAdmin){
	this.age= age
	}
}
```

> [!question] init bock이란?

init은 kotlin의 초기화 블록이다.
primary 생성자가 인스턴스화 되면 실행된다.
secondary 생성자가 호출되면 primary생성자 다음에 실행된다.
- primary -> init -> scondary

> [!question] data클래스란? 장점은?

data클래스는 data를 보유하고 있는 집합을 표한하기 위해 사용한다.

- `equals()`
- `hashCode()`
- `copy()`
- `toString()`
위 함수들을 제공하고 있다.

**장점**
boilderplace Code를 줄여주어 가독성이 올라간다.

1. 동등성 비교시 프로퍼티 값 비교를 지원한다.
	(다른 객체여도 값이 같다면 같다.)
2. toString을 자동으로 구현해준다.
3. 구조 분해 선언도 가능하다.

**제약사항**
- 적어도 하나이상의 매개변수가 primiary 생성자에 있어야 한다.
- abstract, open, sealed, inner는 허용되지 않는다.
- interface만 data class에 의해 구현 될 수 있다.
- 상속이 불가능하다.

> [!question] inline vs infix  function

- inline functions
	- 호출된 익명함수/람다식에 대한 객체 할당을 방지하여 메모리 오버헤드를 줄이는데 이용된다.
	- 런타임에 호출하는 함수에 해당 함수 body를 제공한다.
	  이로 인해 바이트코드의 크기는 약간 증가하지만, 메모리를 많이 절약한다.
- infix functions
	- 중위연산자
	- (하나의 매개변수에만 사용할 수 있다.)

> [!question] lazy vs lateinit?

둘다 propery를 초기화를 지연하는데 이용한다.
- lateinit
	- var 에 사용되며, 나중에 var값을 설정함
- lazay는 val에도 쓰일 수 있다.
	- 필요한 경우 런타임에서 생성된다.

> [!question] kotlin vs java

**1. Null safety**

- kotlin의 모든 변수는 null값을 허용하지 않는다.
- 모든 변수에 null이 할당될 수 있기 때문에 null 값을 이용하는 개체를 참조할때 `NullPointerExceptions`가 발생하는지 *개발자가 직접 관리*해야 한다.

**2. Coroutines Support**

- 코틀린은 스레드를 차단하지 않고, 실행을 중지할 수 있는 코루틴을 지원한다.
- 자바는 스레드 생성, 실행이 가능하지만 관리가 쉽지 않다.

**3. Data classes**
- 코틀린은 data class를 지원하여, 보일러플레이트 비용을 줄일 수 있다.

**4. Functional Programming**
- 코틀린은
	- lambda expressions
	- operator overloading
	- higher-order functions
	- lazy evaluation
	등 다양한 기능을 가진 절차형, 함수형 프로그래밍 언어이다.
- Java
	- Java 8 까지 함수형 프로그래밍을 지원하지 않는다.

**5. Extension Functions**
- 코틀린은 기존 클래스에 새로운 기능을 추가할 수 있다.
- 자바는 기존 클래스에 새로운 기능을 추가하려면, 상속을 통해 구현해야 한다.

**6. Data Type Inference**
- kotlin은 변수의 type을 명시적으로 지정하지 않아도 괜찮다.
- java는 type을 명시적으로 선언해야 한다.

**7. Smart Casting**
```kotlin
fun smartCast(value:Any){
  when(value){
    is Int -> println(value + 2)
    is String -> println(value)
    else -> return
  }
}
```

- 코틀린은 변수의 타입을 직접 검사하지 않고, 컴파일러가 알아서 검사하고, 캐스팅한다.
- 자바는 변수의 type을 직접 검사하고 적절하게 casting해야 한다.

**8. Checked Exceptions**
```kotlin
// kotlin case1

fun doSomething(){
  service.somethingA()
}

// kotlin case2
@Throws(AException::class)
fun doSomething(){
  service.somethingA()
}
```

```java
public void doSomething(){
  try{
    service.somethingA()
  } catch(AException e){
    // exception process
  }
}

// java case2

public void doSomething() throws AException
  service.somethingA()
}
```
- kotlin은 checked exceptions이 없다.
	따라서 개발자가 선언하거나 catch할 필요가 없다.
- Java에는 checked exceptions을 지원하며, 이를 직접 선언하고 관리해야한다.

> [!question] mutableList vs immutableList 더 좋은것은?

단순히 view만 한다면 immutable list가, colletion이 변경될 경우 mutable list가 좋다.

**immutable list의 장점**
- immutable하기때문에 상태가 변경되지 않는다.
	- 함수형 프로그래밍 기법을 추구한다.
	- side effect가 없기때문에, 이해하고 디버깅하기 더 쉬울 수 있다.
	- 다중 스레드 시스템에서, write접근이 필요 없기 때문에, 리소스 경쟁 조건을 유발하지 않는다.
단점
- 추가 / 삭제/ 변경을 위해 collection 전체를 복사하는것은 너무 비싸다.


>[!question] lateinit은 무엇인가요?

```kotlin
lateinit var test:String

fun testFunction(){
	test = "test"
	println(test.length) // 9
}
```

생성자에서 변수를 초기화 하지 않고, 나중에 초기화 하려면 late init키워드를 이용해서 변수를 선언한다.
- 초기화 되기 전까지는 메모리 할당이 되지 않는다.
- lateinit은 나중에 초기화 되므로, `val`을 이용할 수 없다.
- `primitive type`이나 `nullable` 은 쓸 수 없다.
- *만약 초기화 되기 전에 접근하면 예외가 발생한다.*
---
- 생성자 외부에서 독립적으로 초기화 되는 주입된 클래스 변수(DI)
- 단위 테스트에서 @Before주석이 달린 함수에서 테스트 환경 변수

> [!question] lazy initialization은 무엇인가요?

lazy initialization을 이용하여 객체를 선언하면, 객체가 이용될 때 한번만 객체가 초기화 된다. 만약 이용하지 않으면, 초기화도 되지 않는다.
 [[Kotlin Lazy Initialization]]

> [!question] scope functions은 무엇인가요?
> 

Kotlin 표준 라이브러리에는 객체 context 내에서 코드 블록 실행을 지원하는 많은 함수가 있다.
람다 식을 이용하여 객체에서 이러한 함수들을 호출하면 임시 scope가 생성되는데, 이를 scope function이라 부른다.

![scopeFunction 정리](https://img1.daumcdn.net/thumb/R1280x0.fpng/?fname=http://t1.daumcdn.net/brunch/service/user/1OLd/image/hvIh5c47ZsceVhFAPw4VvfzluKw.png)

[[kotlin scope Function]]


> [!question] backing field 는 무엇인가요?

backing fied는 접근자(getter/setter) 내부에만 이용할 수 있는 자동 생성된 field이다.
custom getter/setter를 이용할 때, 필요한 경우 field 식별자로 접근할 수 있다.

```kotlin
var marks: Int = someValue
get() = field
set(value){
	field = value
}
```


>[!question] SAM 인터페이스

- Single abstract method: 단일 추상 메소드

SAM 인터페이스란
- 추상 메소드가 단 1개 있는 인터페이스
- ==함수형 인터페이스==라고도 한다.(Funcational interface)

>[!tip] 코틀린에서 함수형 인자로 받는 Java함수를 호출 할 경우, 인터페이스 객체 대신 람다를 넘길 수 있다.
>```kotlin
>button.setOnClockListener{ println("객체 대신 람다를 넘기고 있음") }
>```
>- 람다를 함수형 인터페이스의 인자로 전달할 때,
>  컴파일러가, 람다에 대해 익명 객체를 생성해 메소드에 넘김
>- 익명객체를 직접 생성해서 넘길 땐, 해당 코드를 수행할 때마다 익명 객체가 새로 생성되지만, 람다를 사용할 땐 내부적으로 생성된 1개의 인스턴스를 재사용한다.
>- 이 동작은 Java메소드를 코틀린에서 호출 할 때 쓰이는 방식이고, 대부분의 코틀린 함수들은 람다를 넘겼을 때 다른방식으로 동작한다.
>  (익명 객체를 생성하거나 하진 않는다. 코틀린에는 함수타입이 따로 있기 때문)



>[!question] sealed class

[[sealed class]]
`sealed class`는 상속을 제한하는 데 사용된다.
서브클래스는 같은 패키지 내에서 선언되어야 하며, 한정된 수의 서브클래스를 가질 수 있습니다.
주로 상태를 나타내거나 특정 계층 구조의 클래스를 구현할 때 사용됩니다. 예를 들어, 상태를 표현하는 클래스 계층 구조에서 각 상태를 나타내는 서브클래스들을 봉인 클래스로 선언할 수 있습니다.

sealed class와 enum의 차이
-  `sealed class`는 상속을 제한하고 상태를 나타내는 클래스 계층을 만들 때 사용되며, `enum class`는 상수 목록을 정의하고 명시적인 값 중 하나를 선택할 때 사용됩니다.



>[!question] 꼬리재귀

조건에 맞는 재귀함수를 for문으로 변경하여 최적화를 해줍니다.