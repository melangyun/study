객체 지향 설계에서 많이 사용하는 패턴 중 하나. 객체가 할 수 있는 일을 다른 객체에 위임하는 패턴이다.
Kotlin에서는 이 패턴을 매우 간단하게 구현할 수 있도록 언어 수준에서 지원한다.

# 사용 목적
1. 책임 분리: 여러 클래스에 분산된 로직을 하나의 클래스에 집중시키지 않고, 필요한 기능을 다른 객체에 위임하여 코드의 가독성과 유지보수성을 높인다.
2. 재사용성: 공통된 기능을 여러 클래스에서 재사용 할 수 있도록 한다.

```kotlin
interface Printer {
  fun printMessage(message: String)
}

class ConsolePrinter: Printer{
  override fun printMessage(message: String){
    println(message)
  }
}

class FilePrinter: Printer {
  override fun printMessage(message:String){
    println("파일에 쓰기: $message")
  }
}

//ReportGenerator 클래스는 Printer를 구현하지만, 실은 구현받은 생성자에게 받은 printer객체에게 위임한다.
class ReportGenerator(printer: Printer): Printer by printer

fun main(){
  val consolePrinter = ConsolePrinter()
  val reportGeneratorWithConsolePrinter = ReportGenerator(consolePrinter)
  reportGeneratorWithConsolePrinter.printMessage("Hello, Console")

    val filePrinter = FilePrinter()
    val reportGeneratorWithFilePrinter = ReportGenerator(filePrinter)
    reportGeneratorWithFilePrinter.printMessage("Hello, File")
}
```

이렇게 하면 ReportGenerator 클래스는 Printer의 구체적인 구현을 신경쓰지 않고, 다양한 Printer구현체를 사용할 수 있다.

> [!question] Delegate패턴과 [[전략패턴(Strategy Pattern)]]은 뭐가 다를까?
> Delegate패턴은 주로 기능의 재사용과 책임 분리에 중점을 두며, 클라이언트 객체는 위임 객체의 메서드를 직접 호출한다.
> 전략패턴은 알고리즘의 캡슐화와 `교환 가능성`에 더 중점을 두며, 클라이언트 객체는 전략 객체를 통해 메서드를 호출하고 런타임에 변경할 수 있다.

> [!example] kotlin의 by키워드를 활용한 로깅

```kotlin
import org.slf4j.Logger  
import org.slf4j.LoggerFactory  
  
// 로거 인스턴스 생성을 위한 제네릭 확장 함수  
fun <A : Any> A.logger(): Lazy<Logger> = lazy { LoggerFactory.getLogger(this.javaClass) }  
  
// 클래스 내부에서 위임을 통해 로그 인스턴스 사용  
class MyClass {  
    private val log by logger()  
  
    fun performAction() {  
        log.info("Action performed")  
    }  
}
```
- `by` 키워드 사용은 개발자가 코드를 보다 효과적이고 깔끔하게 관리할 수 있도록 돕는다.

---
[Kotlin 자주 사용하는 패턴 정리](https://cheese10yun.github.io/kotlin-pattern/)