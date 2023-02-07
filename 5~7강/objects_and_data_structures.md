# 6장 객체와 자료구조

> 이번 내용은 class / interface 관련 깊은 내용입니다. 따라서 javascript를 위주로 다루는 front-end 입장에서 이해하기가 어려우며 사용성(javascript도 class 문법 / 접근제어자 있음)도 떨어집니다. 이해의 편의를 위해 순서를 일부 변경했으며 자료구조를 자료구조체라고 부르겠습니다.

## 자료/객체 비대칭

|               |  객체  | 자료구조체 |
| :------------ | :----: | :--------: |
| `변수`        | 비공개 |    공개    |
| `함수`        |  공개  |    없음    |
| `메소드 추가` | 어려움 |    용이    |
| `자료 추가`   |  용이  |   어려움   |

- 절차적인 도형 클래스

```
public class Square {
	public double side;
}

public class Circle {
	public double radius;
	public double width;
}

public class Geometry {
	public final double PI = 3.141592653585793;

    public double area(Object shape) throws NoSuchShapeException {
    	if(shape instanceOf Square) {
    		Square s = (Square)shape;
    		return s.side * s.side;
    	}
		else if(shape instanceOf Circle) {
			Circle c = (Circle)shape;
			return PI * c.radius * c.radius
		}
	}

}

```

여기서 Rectangle이라는 새로운 도형을 추가하고 싶다면

1.  새로운 도형 자료구조체 생성
2.  Geometry 클래스에 함수를 수정
    이와같이 번거롭게 두 가지 작업을 거쳐야합니다.

반면에 halfArea(도형의 부피의 반을 구하는 함수)를 추가하려면 Geometry 클래스에 함수를 추가하고 도형 클래스는 아무 영향도 받지 않습니다.

- 객체 지향적인 도형 클래스

```
public class Square implements Shape {
	public Point topLeft;
	public double side;

    public double area() {
    	return side*side;
    }

}

public class Circle implements Shape {
	public Point center;
	public double radius;
	public double width;

    public double area() {
    	return PI*radius*radius;
    }

}
```

halfArea를 추가하려면

1.  Geometry interface에 함수 추가
2.  각 도형 class 수정

이렇게 번거로운 작업을 진행해야합니다.
반면에 새 도형을 추가해도 기존 함수에 아무런 영향을 미치지 않습니다.

## 자료 추상화

> 객체에 getter/setter를 생성한다면 변수를 외부로 노출시키는 것이므로 추상화가 필요합니다. 추상 인터페이스를 제공해 사용자가 구현을 모른 채 자료의 핵심을 조작할 수 있어야 진정한 객체입니다. 변수를 숨기는 이유는 외부 접근자가 함부로 수정하면 안되기 때문입니다.

react에서 custom hook을 예로들면

```
const [input, onChangeInput] = useInput('');
```

useInput 이라는 custom hook은 onChange 함수와 input이라는 state를 제공하며 state는 onChangeInput으로만 수정 가능합니다.

- 구체적인 Vehicle 클래스 (구현을 외부로 노출)

```
public interface Vehicle {
	double getFuelTankCapacityInGallons();
	double getGallonsOfGasoline();
}
```

> 무분별한 함수는 오히려 숨겨야하는 자료를 노출시키는 행위 입니다.

- 추상적인 Vehicle 클래스 (구현을 완전히 숨김)

```
public interface Vehicle {
	double getPercentFuelRemaining();
}
```

자료를 세세하게 공개하기보다는 추상적인 개념으로 표현해야 하며 interface, getter/setter 함수만으로는 추상화 시켰다고 할 수 없습니다.

## 디미터 법칙

> 메소드가 반환하는 객체의 메소드를 사용하면 안 됩니다. 객체는 조회 함수로 내부를 공개하면 안 된다는 의미이며, 사용 시 내부구조를 숨기지 않고 노출하는 셈입니다.

### 기차 충돌

> 여러 객체가 한 줄로 이어진 기차처럼 보이는 조잡한 코드입니다.

```
String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();

```

- ctxt, opts, scratchDir이 객체라면 디미터 법칙 위반

```
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
String outputDir = scratchDir.getAbsolutePath();
```

- txt, opts, scratchDir이 자료 구조라면 내부 구조를 노출하므로 디미터 법칙이 적용되지 않음.

```
final String outputDir = cxtx.opts.scratchDir.absolutePath;
```

코드를 위와 같이 구현했다면 디미터 법칙을 거론할 필요가 없어집니다.

### 잡종 구조

> 절반은 객체, 절반은 자료구조체인 경우 잡종 구조라고 합니다. 양쪽에서 단점만 모아 놓은 피해야 할 구조입니다.

## 자료 전달 자료구조체

- DTO - 공개 변수만 있고 함수가 없는 클래스

- Bean - 비공개 변수와 getter, setter가 있는 클래스
  (저자는 순수주의자들이나 만족시키는 것이라고 함)

- 활성 레코드 - 공개변수가 있거나 비공개 변수와 getter, setter있지만 보통 탐색 함수가 있는 자료구조체를 말합니다. 단, 그외의 비지니스 로직이 들어가면 잡종 구조가 됩니다.
