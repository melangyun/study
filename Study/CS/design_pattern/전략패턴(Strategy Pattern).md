[[10분 테코톡] 📣 완태의 전략패턴](https://youtu.be/vNsZXC3VgUA)
- **전략**: 특정한 목표를 수행하기 위한 행동 계획
- **디자인 패턴**: (소프트웨어) 디자인 + (공통적으로 마주치는 문제를 해결하는 방법의) 패턴
- **전략 패턴**
	- 디자인 패턴중에 하나로, 객체 할  수 있는 **행위**를 각각의 **전략**으로 만들어 놓고 사용하며, **동적으로 전략 수정**이 가능한 패턴
	- **전략 패턴의 의도**
		- 동일 계열의 *알고리즘 군을 정의*하고(walk, run, fly, rocket)
		- 각 알고리즘을 *캡슐화* 하며 (Move Strategy)
		- 이들을 *상호 교환*이 가능하도록 만듭니다.


```JAVA
public interface MoveStrategy{
	void move();
}
```

```JAVA
public class Walk implements MoveStrategy{
	@Override
	public void move(){
		System.out.print("걸어서 배달합니다.")
	}
}
```

```JAVA
public class Run implements MoveStrategy{
	@Override
	public void move(){
		System.out.print("뛰어서 배달합니다.")
	}
}
```

```JAVA
public interface TemperatureStrategy{
	void temperature();
}
```

```JAVA
public class Cold implements TemperatureStrategy{
	@Override
	public void temprature(){
		System.out.print("차갑습니다.")
	}
}
```

```JAVA
public class Warm implements TemperatureStrategy{
	@Override
	public void temprature(){
		System.out.print("따듯합니다.")
	}
}
```

### 상호 교환 기능 추가
```JAVA
public abstract class Robot{
	private MoveStrategy moveStrategy;
	private TemperatureStrategy temperatureStrategy;
	
	public Robot(MoveStrategy moveStrategy, TemperatureStrategy temperatureStrategy){
		this.moveStrategy = moveStrategy;
		this.temperatureStrategy = temperatureStrategy;
	}
	
	public void move(){
		moveStrategy.move();
	}

	public void temperature(){
		temperatureStrategy.temperature();
	}

	// Setter를 추가해줌으로써 객체 생성 후 전략을 변경
	public void setMoveStrategy(MoveStrategy moveStrategy){
		this.moveStrategy = moveStrategy;
	}

	public void setTempratureStrategy(TemperatureStrategy temperatureStrategy){
		this.temperatureStrategy = temperatureStrategy;
	}
}
```

```JAVA
public class Main{
	public static void main(String[] args){
		Robot robot = new Robot(new Walk(), new Cold());

		// Walk, Cold
		robot.move();
		robot.temperature();

		// Fly, Cold
		robot.setMoveStrategy(new Fly());
		robot.move();
		rovot.temperature();

		// Fly, Hot
		robot.setTemperatureStrategy(new Hot();
		robot.move();
		robot.temperature();
	}
}
```

- JDK의 compare는 전략패턴으로 구현된것

<iframe width="560" height="315" src="https://www.youtube.com/embed/90ZDvHl8ROE?si=MtM3bNOXyDLSP9rZ&amp;controls=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

**OCP**
1. 상속(is-a)
2. 컴포지션(has-a)
	- **깨지기 쉬운 상위 클래스 문제**
		상속은 하위클래스가 상위클래스의 기능과 밀접하기 때문에 상위가 바뀌면 하위에 영향이 매우 크다
	- **컴포지션 적용법**
		1. 변경(확장)될 것과 변하지 않을 것을 엄격히 구분
		2. 이 두 모듈이 만나는 지점에 인터페이스를 정의
		3. 구현에 의존하기 보다 정의한 인터페이스에 의존하도록 코드를 작성
		-> 자바의 List인터페이스