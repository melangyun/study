[\[kotlin\] object & companion object](https://parade621.tistory.com/37)

# Object
## 1. object declaration(선언식); Singleton

```kotlin
object Singleton {..}

val singleton = Singleton
```

선언된 싱글톤은 객체명만으로 사용이 가능하다.

## 2. object expressions(표현식)

선언식과 달리 object를 표현식으로 사용하면, 익명 객체(anonymous object)로 사용 가능하다.


- 익명 클래스의 객체로 바로 생성하는 경우
```kotlin
val user = object{
	val name = "name"
	val age = 29
}

println(user.name)
```

- 추상 클래스, 인터페이스의 구현체를 익명 클래스의 객체로 구현하고자 하는 경우
```kotlin
interface Human {
	val name: String
	val age: Int
}

val user = object: Human{
	override val name = "이름"
	override val age = 20
}
```

> 아래 예제는 싱글톤이 아니다.
> 호출 할 때 마다 새로운 인스턴스가 생성되기 때문!


# companion object

companion object는 클래스 안에 정의된 일반 객체이다.

- [!] 코틀린 언어는 자바의 static 을 지원하지 않기때문에, 클래스 안에는 static 멤버가 없다!
> [!tip] 최상위 함수와 객체 선언을 활용한다.
> 클래스 안에 companion object를 정의 후, 그 안에 클래스의 프로퍼티나 메소드를 선언한다면, 자바의 static 호출 구문과 동일하게 외부에서 접근할 수 있다.

> [!check] companion object선언으로 private 생성자를 호출하기 좋다.
> 자신을 포함한 클래스의 모든 private 멤버에 접근할 수 있기 때문에 ==팩토리 패턴을 구현하기 가장 적합한 위치==이다.


```kotlin
class User {
  val name: String
  
  constructor(email:String){
	  name = email.substringBefore("@")
  }

  constructor(naverEmailId: String){
	  name = getNaverName(naverEmailId)
  }
}
```

```kotlin
class User private constructor(val name: String){
	companion object{
		fun newEmailUser(email:String)
			= User(email.substringBefore("@"))
		fun newNaberUser(naverEmail:String)
			= User(getNaberEmail(naverEmailId))
	}
}
```

