- `@Primary`는 여러의 빈 중 <u>기본값</u>으로 사용할 빈을 지정하는 어노테이션. 동일한 타입의 빈이 여러 개 있을 때 특별시 `@Qualifier`로 지정하지 않으면 `@Primary`로 지정된 빈을 지정한다.
- 주로 애플리케이션에서 특정 구현이 다른 구현보다 더 자주사용할 경우 그 구현에 대해 `@Primary`를 붙여 기본 빈으로 설정

```kotlin
interface NotificationService {
    fun sendNotification(message: String)
}

@Service
@Primary // 기본 주입
class EmailNotificationService : NotificationService {
    override fun sendNotification(message: String) {
        println("Sending email notification: $message")
    }
}

@Service
class SmsNotificationService : NotificationService {
    override fun sendNotification(message: String) {
        println("Sending SMS notification: $message")
    }
}
```
이 경우 NotificationService 타입의 빈이 주입되는 곳에서 별도로 `@Qualifier`를 사용하지 않으면 EmailNotificationService가 기본적으로 주입된다.

# @Qualifier
여러개의 빈 중 특정 빈을 명시적으로 선택하여 주입하는 어노테이션. 명확하게 어떤 빈을 주입할지 지정 

우선도: `@Primary` < `@Qualifier`


