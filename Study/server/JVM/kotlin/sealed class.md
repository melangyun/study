# sealed class의 등장 배경

여러개의 Class들이 하나의 부모 Class를 상속 받았다고 했을 때, 컴파일러는 부모 Class를 상속받은 자식 Class들이 있는지 알지 못한다.

```kotlin
abstract class PersonState

class Running: PersonState()
class Walking: PersonState()
class Idle: PersonState()

fun getStateMessage(personState: PersonState): String {
  return when(personState){
	is Running -> "Person is running"
	is Walking -> "Person is walking"
	is Idel -> "Person is doing nothing"
	// 하지만 이 경우 에러가 발생한다.
	// 'when' expression must be exhaustive, add necessary 'else' branch
  }
}
```
> 왜 else branch 가 있어야 하는가?
> *컴파일러가  PersonState를 상속받는 하위 클래스의 종류를 알지 못하기 때문이다.*

`personState`를 사용하는 부분이 여기만 있다면 다행이지만, 위의 코드는 관리되지 않는 코드로 전략해벌릴것이다.

# sealed class

`seald class`란 추상클래스로 상속받는 자식클래스의 종류를 제한하는 특성을 가지고 있다. 즉, 컴파일러에서 sealed class의 자식클래스가 어떤 것이 있는지 알 수 있다.

```kotlin
seald class PersonState

class Running: PersonState()
class Walking: PersonState()
class Idle: PersonState()

fun getStateMessage(personState: PersonState):String {
	return when(personState){
		is Running -> "Person is running"
		is Walking -> "Person is walking"
		is Idel -> "Person is doing nothing"
	}
}
```
> sealed class 를 사용하면 오류가 생기지 않는다. PersonState의 자식 클래스는 세가지만 있는 것을 알고 있기 때문이다. 따라서 when 에 else brnch를 사용하지 않고도 필요한 메세지만 수신할 수 있다.

앱을 확장시킬 때도 관리되는곳을 컴파일러가 찾아주기 때문에 유용하다.

## sealed class의 특징

- 같은 패키지의 자식 클래스만 상속이 가능하다.
  > 컴파일러가 모든 패키지를 돌면서 자식을 찾는건 너무 리소스를 많이 소모하는 작업이다. 따라서 sealed class는 자식 클래스에 대한 선언을 같은 패키지 내로 제한한다.
- 추상 클래스고 직접 객체 인스턴스 생성이 불가능하다.




---

[\[kotlin\] sealed class란 무엇인가?](https://kotlinworld.com/165)