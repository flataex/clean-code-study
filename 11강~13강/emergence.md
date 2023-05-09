# 12장. 창발성

창발성이란? 단순한 결합이 복잡한 결과를 나타내는 것

## 창발적 설계

어떤 규칙과 원칙에 따라 설계하면, 그것들이 모여 **좋은 거시적 결과**가 나타난다.

# 켄트 백의 단순한 설계

켄트 백은 다음의 규칙을 따르면 '단순한' 설계라고 말하였다. (중요도 순)

1. 모든 테스트를 실행
2. 중복 제거
3. 개발자의 의도 표현
4. 클래스와 메서드 수를 최소로 줄임

## 1. 모든 테스트를 실행하라

문서로는 완벽히 설계했지만, 시스템이 의도한 대로 돌아가는지 검증할 간단한 방법이 없다면, 문서 작성을 위해 투자한 노력에 대한 가치는 인정받기 힘들다.

테스트가 가능한 시스템(모든 테스트를 항상 통과하는 시스템)을 만들려고 애쓰면 설계 품질이 높아진다.

- DIP 원칙 적용
- 의존성 주입
- 인터페이스
- 추상화

## 2~4. 리팩터링

테스트 케이스가 있기 때문에 시스템이 깨질까 걱정할 필요가 없다.

리팩터링 단계에서는 소프트웨어 설계 품질을 높이는 기법이라면 무엇이든 적용해도 괜찮다.

- 중복 제거
- 개발자의 의도 표현
- 클래스와 메서드 수를 최소로 줄임

### 중복 제거

중복은 추가작업, 추가위험, 불필요한 복잡도를 뜻한다.

```javascript
// X
function getLength(dataArray) {
  return dataArray.length;
}

function isEmpty(dataArray) {
  return dataArray.length === 0;
}
```

```javascript
// O
function getLength(dataArray) {
  return dataArray.length;
}

function isEmpty(dataArray) {
  return getLength(dataArray) === 0;
}
```

```javascript
async function doSomethingWithData(db, onSuccess, onFailed) {
  try {
    await db.connect();
    const data = await db.query(`SELECT * FROM SomeTable`);
    onSuccess(data);
  } catch (error) {
    onFailed(error);
  } finally {
    await db.unconnect();
  }
}
```

### 개발자의 의도 표현

개발자의 의도를 분명히 표현해야 다른사람이 그 코드를 이해하기 쉬워진다. 그래야 결함이 줄어들고, 유지보수 비용이 적게 든다.

- 좋은 이름 선택
- 함수와 클래스 크기를 가능한 한 줄인다.
- 표준 명칭을 사용한다. (prefix)
- 단위 테스트 케이스를 꼼꼼하게 작성한다

### 클래스와 메서드 수를 최소로 줄임

클래스와 메서드 크기를 줄이자고 조그만 클래스와 메서드를 수없이 만드는 사례가 많음.

타협점을 찾아 실용적인 방안을 사용해야 함.

클래스와 메서드의 크기를 작게 유지하면서 동시에 시스템 크기도 작게 유지하는 것이 목표.

하지만 이는 가장 낮은 우선순위이며, 테스트 케이스를 만들고 중복을 제거하고 의도를 표현하는 작업이 더 중요함
