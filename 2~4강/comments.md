# 4. 주석

## 개요

> 나쁜 코드에 주석을 달지 마라. 새로 짜라.
>
> \- 브라이언 W. 커니핸, P.J. 플라우거

### 주석을 지양해야 하는 이유

- 프로그래머들이 주석을 유지하고 보수하기란 현실적으로 불가능하기 때문
- 주석이 코드의 변화를 따라가지 못하면 잘못된 정보를 전달할 수 있음

### 필요악

주석은 필요악이다.

주석을 사용하기보다 코드로 의도를 표현할 방법을 찾아야 한다.

- 명확한 변수명
- 짧고 간결한 함수

### 주석 대신 코드로 의도를 표현한 예시

- 주석으로 의도를 표현 (x)
  ```javascript
  // 유저가 거래를 할 자격이 되는지 검사한다.
  if(user.secuLevel ===4 && kycDone && !needKycRemind)
  ```
- 코드로 의도를 표현 (o)
  ```javascript
  if(isUserCanTrade(user))
  ```

## 좋은 주석

### 법적인 주석

```javascript
// Copyright (C) 2019~2023 by FlataEx, Inc. All rights reserved.
// MIT License
```

회사가 정립한 구현 표준에 맞춰 법적인 이유로 특정 주석을 넣으라고 명시하는 경우.

### 정보를 제공하는 주석

```javascript
// 영어만 허용
const validate = /^[a-zA-Z]*$/;
```

기본적인 정보를 주석으로 제공한다.

이왕이면 코드를 분리하여(ex. 함수로 분리) 주석이 필요 없도록 한다.

### 의도를 설명하는 주석

코드에서 개발자의 결정에 깔린 의도를 설명한다.

예시)

1. 특정 알고리즘을 사용한 이유
2. 어떠한 로직을 추가하였는데, 추가한 이유를 코드로써 설명하기 어려운 경우

### 의미를 명료하게 밝히는 주석

```java
assertTrue(a.compareTo(a) == 0); // a == a
assertTrue(a.compareTo(b) != 0); // a != b
assertTrue(ab.compareTo(ab) == 0); // ab == ab
assertTrue(a.compareTo(b) == -1); // a < a
```

인수나 반환값이 표준 라이브러리나 변경하지 못하는 코드에 속하는 경우 의미를 명료하게 밝히기 위해 사용한다.

다만 그릇된 주석을 달지 않도록 상당히 조심해야 한다.

### 결과를 경고하는 주석

```javascript
// 다음 코드는 사이드이펙트를 충분히 고려 후 수정하시오.
const appSettings = {
  ...
}
```

### TODO 주석

```javascript
/**
 * TODO: KYC 재이행 대상자에 대한 기획 수정 예정, 개발 보류
 * /
```

TODO 주석은 개발자가 필요하다 여기지만 당장 구현하기 어려운 업무를 기술한다.

주기적으로 점검하여 필요없는 TODO 주석은 제거한다.

### 중요성을 강조하는 주석

```javascript
// 문자열 양쪽에 공백이 있을 경우 API 에러 발생.
const nickname = event.current.value.trim();
```

### 오픈소스 라이브러리에서 JSDoc

여느 주석과 마찬가지로 독자를 오도하거나, 잘못 위치하거나, 그릇된 정보를 전달해서는 안됨.

## 나쁜 주석

대다수 주석이 이 범주에 속한다.

허술한 코드를 지탱하거나, 엉성한 코드를 변명하거나, 미숙한 결정을 합리화하는 등의 경우이다.

### 주절거리는 주석

특별한 이유 없이 의무감으로 혹은 프로세스에서 하라고 하니까 마지못해 다는 주석

### 같은 이야기를 중복하는 주석

```javascript
// 유저가 거래 가능 상태인지 검사하고
// 거래 가능할 시, 거래 요청을 보낸다.
const trade = () => {
  if (!isUserCanTrade()) return;

  makeTradeRequest();
};
```

주석이 코드의 내용을 그대로 중복하는 경우이다.

### 오해할 여지가 있는 주석

주석에 "살짝 잘못된 정보" 가 담긴 경우.

### 의무적으로 다는 주석

```javascript
/**
 * 직원을 추가한다.
 * @param {string} name - 직원 이름
 * @param {string} age - 직원 나이
 * @param {string} job - 직원 직무
 */
const addEmployee = (name, age, job) => {
  ...
}
```

모든 함수에 Javadocs(JSDocs)를 다는 것과 같은 행동은 코드를 복잡하게 만들며, 거짓말을 퍼뜨리고, 혼동과 무질서를 초래한다. (유지보수가 되지 않을 때 얘기일까요..?)

### 이력을 기록하는 주석

```javascript
/**
 * 변경이력
 * 12-Nov-2021 : setting 객체 수정
 * 16-Nov-2021 : 부동소수점 버그 수정
 * ...
 * ...
 * ...
 */
```

오늘날에는 깃으로 관리하고 있으므로 해당사항 없음

### 있으나 마나 한 주석

```javascript
/** 현재시간 객체 */
const now = new Date();
```

너무 당연한 사실을 언급하는 주석.

개발자가 주석을 무시하는 습관에 빠질수 있게 함.

### 무서운 잡음

```typescript
interface MyPageModel {
  // 닉네임
  nickname: string;
  // 이메일
  email: string;
  // 닉네임
  phone: string;
  ...
  ...
  ...
}
```

단순히 주석을 추가해야 한다는 강박에서 실수(잡음)가 발생하였다.

### 함수나 변수로 표현할 수 있다면 주석을 달지 마라

- before
  ```java
  // 전역 목록 <smodule>에 속하는 모듈이 우리가 속한 하위 시스템에 의존하는가?
  if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))
  ```
- after
  ```java
  ArrayList moduleDependees = smodule.getDependSubsystems();
  String ourSubSystem = subSysMod.getSubSystem();
  if (moduleDependees.contains(ourSubSystem))
  ```

### 위치를 표시하는 주석

```javascript
/* Custom CSS */
```

코드에서 특정 위치를 표시하려 사용하는 주석.

### 닫는 괄호에 다는 주석

```javascript
if(...){
  for (...){
    ...
  } // for
} // if
```

닫는 괄호에 주석을 다는 것 대신에 함수의 길이를 줄이려 시도하자.

### 공로를 돌리거나 저자를 표시하는 주석

```javascript
/**
 * @author minxd95
 * /
```

오랫동안 코드에 방치되어 점차 쓸모없는 정보로 변해간다.

버전관리 시스템을 활용하자. (git)

### 주석으로 처리한 코드

```javascript
let app: FirebaseApp, analytics: Analytics, database: Database;

// if (!getApps().length && typeof window !== 'undefined') {
//   app = initializeApp(firebaseConfig)
//   analytics = getAnalytics(app)
//   database = getDatabase(app)
// }
```

위와 같은 코드는 다른 사람들이 지우기를 주저한다. 그렇게 점점 쌓여만 간다.

버전관리 시스템(git)을 믿고 코드를 삭제하라.

### 전역 정보

```javascript
// 서버를 실행한다. (기본 포트 : 3000)
app.listen(process.env.PORT, () =>
  console.log(`listening on port ${process.env.PORT}`)
);
```

현재 코드와 관련된 주석만 작성하라.

### 너무 많은 정보

흥미로운 역사나 관련 없는 정보를 장황하게 늘어놓는 경우

ex) 코드에서 사용된 알고리즘의 역사

### 모호한 관계

주석과 주석이 설명하는 코드는 둘 사이 관계가 명백해야 한다.

주석 자체가 다시 설명을 요구해서는 안된다.

### 함수 설명 주석

짧고 한 가지만 수행하며 이름을 잘 붇인 함수는 주석이 필요없다.

### 비공개 코드에서 Javadocs(JSDoc)

공개하지 않을 코드라면 Javadocs(JSDoc)는 쓸모가 없다.
