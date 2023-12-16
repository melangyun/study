> 동적 프로그래밍에 대한 이야기를 나누다, Java reflection에 대한 것을 공부하게 되었다.

자바의 Reflecction은 JVM에서 실행되는 애플리케이션의 <u>런타임 동작을 검사하거나 수정할 수 있는 기능</u>이 필요한 프로그램에서 사용된다.
	Reflection을 사용해서 스프링에서는 런타임 시에 개발자가 등록한 빈을 애플리케이션에서 가져와 사용할 수 있게 된다.
> 구체적인 클래스 타입을 모를때 사용하는 방법인데, 내가 짠 코든데 내가 만든 클래스의 이름을 모르는게 말이 되나? 라는 의문이 생길수도 있지만.. 정말 모르는경우가 생긴다..

**예제 코드**

```JAVA
Class c = "foo".getClass();
System.out.println(c); // class Java.lang.String

Set<String> s = new HashSet<Set>();  
Class c2 = s.getClass();  
System._out_.println(c2); //class java.util.HashSet
// 원시타입은 에러

Class c = Class.forName("클래스이름")
// 메소드
Method[] m = c.getMethods();
// 필드
Field[] f = c.getFields();
//구조체
Constructor[] cs = c.getConstructors();
Class[] interfaces = c.getInterfaces();
Calss superClass = c.getSuperClass();
```


**주의사항 및 단점**
Reflection을 사용하지 않고 수행 가능하다면, 사용하지 않는것이 좋다.
- Reflection은 동적으로 해석되는 유형이 포함되므로, JVM 최적화를 수행할 수 없다. 따라서 성능이 떨어지며, 성능에 민감한 어플리케이션에서 자주 호출되는 코드엔 사용하지 않아야한다.
- 보안 제약
- 캡슐화 저해; Reflection은 private한 Property및 method에 엑세스 하는것 과 같이 Relection을 사용하면 예기치 않은 부작용이 발생하여 코드 기능이 저해되고 이식성이 손상 될 수 있다. 또 추상화를 깨뜨려 플랫폼 업데이트시 동작이 변경될 수 있음

---
[참고 링크: 자바 Reflection이란?](https://medium.com/msolo021015/자바-reflection이란-ee71caf7eec5)