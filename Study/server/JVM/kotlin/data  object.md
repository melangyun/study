- bject와 동일히 단일 인스턴스만 생성된다.
- `data class`와 같이 데이터 보존 메서드를 자동으로 생성한다.
	- `toString()`, `hashCode()`, `equals()`메서드가 자동으로 생성된다.
- 불변객체를 선언하는데 적합하다.

```kotlin
data object SingletonDataObject{
  val name: String = "SingleTon"
  val id: Int = 12345
}

fun main(){
  println(SingletonDataObject.name)
  // SingleTon
  println(SingletolnDataObject)
  // SingletonDataObject(name=Singleton, id=12345)
}
```

**장점**
`data class` 와 동일히 주요 메소드를 자동으로 생성한다.
간결히 데이터를 보존하고 단일 인스턴스를 사용하는 경우 코드가 간결해진다.

**주의사항**
단일 인스턴스로만 사용되므로, 여러 인스턴스가 필요한 경우 적합하지 않다.
다른 객체와의 초기화 순서에 주의해야한다.
특히 `companion object`나 다른 `object`의 상호 참조가 발생할 수 있는 경우 주의가 필요하다.

---

> object 를 참조시 초기화 순서의 문제때문에 `NullPointerException`이 유발될 수 있다.

```kotlin
object A {
    val b = B
}

object B {
    val a = A
}
// 이 경우 lazy를 사용하여 초기화 순서 제어가 필요하다.
// 혹은 초기화 블록 `init`을 사용하여 명확히 정의해야한다.
```

> companion object는 클래스가 로드될 때 초기화 되지만, 다른 `object`와의 상호 참조가 있을 경우 문제가 될 수 있다.


```kotlin
class MyClass {
    companion object {
        val a = A
    }
}

object A {
    val b = MyClass()
}

```

