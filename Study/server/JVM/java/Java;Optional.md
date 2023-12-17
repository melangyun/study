Java8에서 도입된 클래스. 값이 존재할 수도 있고, 아닐 수도 있는 컨테이너를 나타냄
*NullPointException*을 방지하고 코드를 더 안전하게 만들 수 있다.

1. 값이 존재하는 경우
	- `Optional` 객체 안에 값을 포함시킨다.
	- `Optional.of(T value)` 또는 `Optional.ofNullable(T value)` 메서드를 사용하여 값을 감쌀 수 있다.
		- `Optional.of`는 매개변수가 null이 아닐때만 유효함
		  > 만일 null이 전달된다면 NullPointerException 발생
		- `Optional.ofNullable` 매개변수가 null도 가능함
		  > 만일 null이 전달되면 빈 `optional` 객체 생성
```java
Optional<String> optional = Optional.of("Hello, World!");
```

2. 값이 없는 경우
	- `Optional .empty()` 메서드를 사용하여 빈 `Optional` 객체를 생성할 수 있음
```Java
Optional<String> emptyOptional = Optional.empty();
```

3. 값의 존재 여부 확인 (`isPresent()`)
```Java
if (optional.isPresent()) {
    // 값이 존재하는 경우 처리
    String value = optional.get();
    System.out.println(value);
} else {
    // 값이 없는 경우 처리
    System.out.println("Value is absent.");
}

```

4. 값의 안전한 추출, 메서드 지원
```java
String value = optional.orElse("Default Value");

optional.ifPresent(val -> System.out.println("Value: " + val));
```
# Java Optional 올바르게 사용하기

## 1.  Optional 변수에 null 할당 하지 말것

반환 값으로 null 을 사용하는 것이 위험하기 때문에 등장한 것이 Optional 이다.
당연히 Optional 대신 null 을 반환하는 것은 Optional 의 도입 의도와 맞지 않는다.

**Optional** 은 내부 값을 **null** 로 초기화한 싱글톤 객체를 **Optional.empty()** 메소드를 통해 제공하고 있다.  
위에서 말한 "결과 없음"을 표현해야 하는 경우라면 **null** 대신 **Optional.empty()**를 반환하는 것이 좋다.

*나쁜예:*
```java
Optional<Member> findById(Long id) { 
  // find Member from db
  if (result == 0) {
	return null;    
	}
}
```

*좋은 예:*
```java
Optional<Member> findById(Long id) {
    // find Member from db
    if (result == 0) {
        return Optional.empty();
    }
}
```

## 2. Optional.get() 호출 전에 Optional 객체가 값을 가지고 있음을 확실히 할 것

Optional 을 사용하면 그 안의 값은 Optional.get() 메소드를 통해 접근 할 수 있는데,만약 빈 Optional 객체에 get() 메소드를 호출한 경우 `NoSuchElementException`이 발생하기 때문에 값을 가져오기 전에 반드시 값이 있는지 확인해야 한다.

*나쁜 예:*
```java
Optional<Member> optionalMember = findById(1);

String name = optionalMember.get().getName();
```

*피해야 하는 예:*
```java
Optional<Member> optionalMember = findById(1);
if (optionalMember.isPresent()) {
    return optionalMember.get();
} else {
    throw new NoSuchElementException(); 
}

```

*좋은 예:*
```java
Member member = findById(1).orElseThrow(MemberNotFoundException::new);

String name = member.getName();
```

피해야 하는 예의 경우엔 반드시 나쁘다고만은 할 수 없지만,이후에 소개할 Optional 의 API를 활용하면 동일한 로직을 더 간단하게 처리할 수 있다.Optional 을 이해하고 있다면 가독성 면에서도 더 낫기 때문에 꼭 필요한 경우가 아니라면 피하는 것이 좋다

## 3. 값이 없는 경우, Optional.orElse() 를 통해 이미 생성된 기본 값(객체)을 반환 할 것


*나쁜 예:*
```java
public static final String USER_STATUS = "UNKNOWN";
// ...
public String findUserStatus(long id) {

    Optional<String> status = ... ; // prone to return an empty Optional

    if (status.isPresent()) {
        return status.get();
    } else {
        return USER_STATUS;
    }
}
```

*좋은예:*
```Java
public static final String USER_STATUS = "UNKNOWN";
// ...
public String findUserStatus(long id) {

    Optional<String> status = ... ; // prone to return an empty Optional

    return status.orElse(USER_STATUS);
}
```

*주의할점:*
`OrElse`는 `Optional`객체가 존재할때도 평가된다. 이는 사용되지 않을때도 평가된다는것이며 성능저하를 일으킬 수 있다. 이 맥락에서는 `orElse()`매개변수(기본 개체)가 이미 생성되어있는(constructed) 경우에만 사용하는 것이 좋다.

```Java
Member member = findById(1).orElse(new Member());
```
- [!] `orElse`의 `Member`생성하는 행위는 Optional에 값이 있건 없건 무조건 실행된다.

## 4. 값이 없으면, Optional.orElseGet() 를 통해 존재하지 않는 기본 객체 반환

*나쁜 예:*
```java
Member member = findById(1).orElse(new Member());
// 값이 있던 없던 new Member()는 무조건 실행됨
```

*좋은 예:*
- [p] `orElseGet`은 `Optional`이 값이 없을때만 실행된다!
	따라서 Optional에 값이 없을 때만 새 객체를 생성하거나 새 연산을 수행하므로 불필요한 오버헤드가 없다. 물론 람다식이나 메소드 참조에 대한 오버헤드는 있겠지만, 불필요한 객체 생성이나 연산을 수행하는 것에 비하면 경미하다.
```java
Member member = findById(1).orElseGet(Member::new);
```

## 5. 값이 없는 경우, Optional.orElseThrow() 를 통해 명시적으로 예외를 던질 것

값이 없는 경우, 기본 값을 반환하는 대신 예외를 던져야 하는 경우도 있다. 이 경우에는 **Optional.orElseThrow()** 를 사용하자.

```java
Member member = findById(1).orElseThrow(() -> new NoSuchElementException("Member Not Found"));

```

- java 10부터는 orElseThrow의 인수 없이도 사용할 수 있다
```java
public final class Optional<T> {
	public T orElseThrow() {
		if(value == null){
			throw new NoSuchElementException("No value present");
		}
		return value;
	}
}
```

## 6. Optional.isPresent() 는 다른 것으로 대체할것

*나쁜 예:*
```java
Optional<Member> optionalMember = findById(1);
if(optionalMember.isPresent()){
	System.out.println("member: " + optionalMember.get());
}
```

*좋은예:*
- [p] `ifPresnt()` 
```java
Optional<Member> optionalMember = findById(1);
optionalMember.ifPresent(System.out::println);
```

- [p] `orElseThrow()`
```java
Member member = findById(1)
	.orElseThrow(() -> new MemberNotFountException("Member not found id: " + 1));
```


## 7. Optional을 필드타입으로 사용하지 말것

`Optional`은 ==반환 타입을 위해 설계된 타입==이다.
`Optional` 을 클래스 필드로 선언하거나, 메서드 인자로 사용하는 것은 Optional의 도입 인도에 반하는 패턴이다.

*나쁜 예:*
```java
public class Member {
	private Optional<String> name;
}
```

*좋은 예:*
```java
public class Member {
	private String name;
}
```

## 8. Optional을 생성자나 메서드 인자로 사용하지 말것

`Optional`을 생성자나 메서드 인자로 사용하면 호출할때마다 `Optional` 을 생성해서 인자로 전달해줘야한다.
굳이 비싼 `Optional` 인자로 사용하지 말고 호출되는 쪽에 `null`체크 책임을 남겨두는 것이 좋다.

*나쁜 예:*
```java
public void increaseSalary(Optional<Member> member, int salary){
// ..
}

increaseSalay(Optional.offNullable(member), 10);
```

## 9. Optional은 비싸기 때문에 과도하게 사용하지 말아야 한다.

> [!tip] 단순히 값 또는 `null`을 얻을 목적이라면 `Optional` 대신 `null`비교를 사용하자

## 10. Optional을 빈 컬렉션이나 배열을 반환하는데 사용하지 말 것

컬렉션이나 배열로 복수의 결과를 반환하는 메서드가 `결과 없음` 을 가장 명확하게 나타내는 방법은 대부분의 경우 빈(empty) 컬렉션 또는 배열을 반환하는 방법이다.

이러한 상황에서 빈 컬렉션이나 배열 대신 `Optional` 을 사용해서 얻는 이점이 있는지 고민해볼 필요가 있다.

> 마찬가지 이유로 Spring data JPA Repository 메서드 선언시 컬렉션을 Optional로 감싸서 반환하는 것은 좋지 않다. 컬렉션을 반환하는 Spring Data JPA Repository 메서드는 null을 반환하지 않고 비어있는 컬렉션을 반환해 준다.

## 11. Optional을 컬렉션의 원소로 사용하지 말 것

## 12. Optional.of()와 Optional.ofNullable()을 혼동하지 말것

`of(X)`는 `X`가 `null`이 아님이 확실할 때만 사용해야 하며, X가 null이면 `NullPointException`이 발생한다.
`ofNullable(X)`는 `X` 가 `null`일 가능성이 있을 때 사용해야 하며, `X`가 `null`이 아님이 확실히면 `of(X)`를 사용해야한다.

## 13. 원시 타입의 Optional에는 OptionalInt, OptionalLong, OptionalDouble 사용을 고려할것

원시타입(primitive type)을 `Optional`로 사용하면 `Boxing`과 `UnBoxing`을 거치면서 오버헤드가 생기게 된다.
반드시 `Optional`의 제네릭 타입에 맞춰야 하는 경우가 아니라면, `OptionalXXX`타입 사용을 고려하는것이 좋다.

>[!tip] 이들은 내부 값을 래퍼 클래스가 아닌 원시 타입으로 갖고, 값의 존재 여부를 나타내는 isPresent 필드를 함께 갖는 구현체이다.

## 14. 내부 값 비교에는 Optional.equals사용을 고려하는것이 좋다.

```java
public boolean equals(Object obj) {  
	if (this == obj) {  
		return true;  
	}  
  
	return obj instanceof Optional<?> other  
			&& Objects.equals(value, other.value);  
}
```

## 15. 값에 대해 미리 정의된 제약사항이 있는 경우는 filter 사용을 고려할것

`Optional.filter`도 스트림처럼 값을 필터링 하는 역할을 한다.
인자로 전달된 predicate이 참인 경우에는 기존의 내부 값을 유지한 `Optional`이 반환되고, 그렇지 않은 경우 비어있는 `Optional`을 반환한다.

이를 활용하여 다음과 같이 구현해 볼 수 있다. (하지만 어느 방법이 맞다고 단정하기는 어렵다.)

```java
private boolean isValidName(String username){
	return Optional.ofNullable(username)
		.filter(this::isIncludeSpace)
		.filter(this::isOverLength)
		.isPresent();
}
```


*기존 방식:*
```java
private boolean isValidName(String username){
	return isIncludeSpace(username) && isOverLength(username);
}
```

---
[\[Java\] Optional 올바르게 사용하기](https://dev-coco.tistory.com/178)
[26 Reasons Why Using Optional Correctly Is Not Optional](https://dzone.com/articles/using-optional-correctly-is-not-optional)