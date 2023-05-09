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
