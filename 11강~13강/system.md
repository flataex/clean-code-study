# 시스템

도시가 적절히 돌아갈 수 있는 이유는 적절한 추상화와 모듈화가 되어 있기 때문이다. 그래서 큰 그림을 이해하지 못하더라도, 개개인이 관리하는 구성요소는 효율적으로 돌아간다. 시스템도 마찬가지로, 관심사를 분리하여 시스템을 깨끗하게 유지할 수 있다.

<br/>

## 관심사 분리

시스템은 **객체를 생성하고 의존성을 연결하는 로직**과 **런타임 로직**이 분리되어야한다.  
아래 예시는 관심사 분리가 되지않은 예시이다.

```java
public Service getService() {
    if(service === null)
        service = new MyServiceImpl();
    return service
}
```

`getService` 메소드는 `생성자 인수`와 `MyServiceImpl`에 의존한다. 런타임 시 `service`가 null이 아니어서 `MyServiceImpl`을 사용하지 않더라도, 의존성을 해결하지 않으면 컴파일되지 않는다. 관심사 분리가 되지 않는 것 역시 메소드가 두가지 이상의 작업을 수행하는, **단일 책임 원칙(SRP)를 깨는 것**에 해당된다.

<br/>

### 의존성 해결 방안

1. Main 분리  
   시스템 생성과 사용을 분리하는 방법으로, 생성과 관련된 로직은 모두 main이나 main에서 호출하는 모듈에서 이루어지고 애플리케이션은 모든 객체와 의존성이 생성되었다는 가정하에 실행된다. 즉 애플리케이션은 main이나 객체 생성에 대해 전혀 모르는 상태이다.

2. 팩토리  
   애플리케이션이 객체 생성 시점을 컨트롤해야하는 경우에 Abstract factory 패턴을 사용한다. main은 객체 생성 로직을 갖고 있고, 애플리케이션은 객체가 필요한 시점에 해당 메소드만 호출한다.
3. 의존성 주입  
   객체 간의 의존성을 자신이 아닌 외부에서 받아 결합도를 낮추는 방법이다.

   ```java
   public class SpellChecker {
       Dictionary dictionary = new KoreanDictionary();
   }
   ```

   위 코드에서 `SpellChecker`는 `KoreanDictionary`에 의존한다. 이를 해결하기 위해 인스턴스를 만들지 않고, **setter 메소드**나 **생성자 인수**를 사용한다.

   ```java
   public class SpellChecker {
       private Dictionary dictionary;

       public SpellChecker(Dictionary dictionary) {
           this.dictionary = dictionary;
       }
   }
   ```

   ```java
   public class SpellChecker {
       private Dictionary dictionary;

       public void setDictionary(Dictionary dictionary) {
           this.dictionary = dictionary;
       }
   }
   ```

<br/>

## 확장

관심사 분리를 통해 소프트웨어 아키텍처를 점진적으로 발전시킬 수 있다.

<br/>

### 횡단 관심사

애플리케이션에 주요 기능 `A, B, C`가 있다고 할 때, `A, B, C`에 `로깅, 보안, 트랜잭션 등`과 같은 영속적인 기능이 공통적으로 포함될 수 있다. 이 공통적인 관심사를 횡단 관심사라고 한다.

AOP(Aspect Of Programming)은 횡단 관심사항의 기능을 모듈화하여 중복을 최소화하면서, 핵심 관심사항에 집중하도록 하는 기법이다.

자바에서 사용하는 관점에는 아래 3가지가 있다.

1. 자바 프록시

2. 순수 자바 AOP 프레임워크

3. AspectJ 관점

###

<br/>

---

#### Reference

[DI(Dependency Injection)란?](https://effortguy.tistory.com/7)
