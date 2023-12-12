왜 지연초기화를 쓰는가?
- 메모리 공간 효율 개선 (Memory Leak 방지)
- 성능 향상 (초기화 지연으로 실행시간 향상)

kotlin의 프로퍼티 지연 초기화는 `lateinit`, `lazy` 2가지가 있다.

# lateinit

초기화 지연 프로퍼티로 초기화를 나중으로 미루기 위해 사용한다.
프로퍼티에 선언하여 사용하고 다음과 같은 제약조건이 있다.

- var 타입만 가능
- non-null 만 가능
- primitive type 불가능
	> default type이 있기 때문에.
- Custom getter/setter 불가능
- 클래스 생성자 인자로 사용 불가능
- 지역 변수로 불가능

# 왜 lateinit을 쓸까?

1. non-null type으로 선언된 프로퍼티는 생성자함수에서 초기화 하는게 일반적이지만 비효율적이다
	> 객체가 인스턴스화 될때 멤버변수의 값을 생성자를 통해 할당하게 되는데 생성자를 통한 할당이 아닌 값의 할당이 일어나기 바로 직전까지 초기화를 지연시키는 것이 lateinit의 목적
2. null check
	만약 프로퍼티에 null을 할당해놓고 쓰게된다면 해당 프로퍼티에 접근시 null check를 항상 해주어야 한다는 문제가 생긴다.

```kotlin
class SampleActivity : AppCompatActivity() {

    private var adapter: Adapter? = null
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_sample)
    }

    override fun onResume() {
        super.onResume()
        adapter?.getItem(0)
    }

    override fun onPause() {
        super.onPause()
        adapter?.getItem(0)
    }
}
```

프로퍼티는 멤버변수에 즉시 할당이 아니라 onCreate, setup함수에서 초기화를 해주는것이 퍼포먼스 측면에 좋다.

```kotlin
class LazyInitialization constructor(
    lateinit var firstMsg: String     // X
) {
    lateinit val secondMsg: String    // X
    lateinit var thirdMsg: String?    // X

    lateinit var count: Int           // X
    lateinit var timeMills: Long      // X
    lateinit var isLoaded: Boolean    // X

    lateinit var msg: String          // O
    lateinit var adapter: UserAdapter // O
}
```

# Lazy

`by lazy`는 읽기전용(Read-Only) 프로퍼티를 유용하게 사용할 수 있게 한다.
`by lazy{ }` 의 코드 초기화 블록은 프로퍼티가 최초로 사용 될 때 해당 블록이 실행된다.
그리고 다음과 같은 제약조건이 있다

- val 타입만 가능
- non-null or null 둘 다 가능
- primitive type 가능
- Custom getter/setter 불가능
- 클래스 생성자 인자로 사용 불가능
- 지역 변수로 불가능

```kotlin
class SampleActivity : AppCompatActivity() {

    private val textview: AppCompatTextView by lazy { 
        findViewById<AppCompatTextView>(R.id.tv_title) 
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_sample)
        textview.text = "Sample"
    }
}
```

textview 의 by lazy 코드 블록은 textview객체에 최초 접근
즉 textview.text = "Sample" 해당 코드에서 초기화 블록이 실행됩니다.
정상적인 안드로이드 액티비티 라이프사이클 안에서 초기화 블록이 실행된다면 Runtime에러가 나지않을 뿐더러 불변 변수인 val 으로 뷰의 인스턴스가 바뀔일도 없습니다.

## Lazy 동기화

동기화 옵션은 3가지다
- Synchronized
	1개의 스레드만 값을 계산할 수 있고 모든 스레드가 같은 값을 읽음
- Publication
	초기화를 여러 스레드가 할 수 있고 처음 생성된 인스턴스만 반환
- None
	아무 동기화 연산을 하지 않음. 단일 스레드


이 중 Default로 SYNCHRONIZED를 사용하고 있다.
성능의 순서는 당연히 아무것도하지않는 NONE 부터 PUBLICATION, SYNCHRONIZED 순서이다

## SYNCHRONIZED

by lazy의 프로퍼티의 value는 동기화 된다. 내부적으로 살펴보면
해당 프로퍼티의 value 가 @Volatile 어노테이션과 synchronized 블록을 통해 변수의 가시성을 보장해주어 동기화 처리되어 있다



---
[\[Kotlin\] Kotlin Lazy Initialization\(초기화 지연\)](https://medium.com/kenneth-android/kotlin-kotlin-lazy-initialization-%EC%B4%88%EA%B8%B0%ED%99%94-%EC%A7%80%EC%97%B0-57b08f0f6860)