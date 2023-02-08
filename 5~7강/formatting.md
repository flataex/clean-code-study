## 형식 맞추기

<br/>  
<br/>

### 적절한 행 길이 유지

<br/>

- 파일 크기가 크지 않아도 커다란 시스템을 구축할 수 있다.  
  파일의 크기를 줄이자!
- 내려 읽어가며 세세한 사실을 파악할 수 있도록 한다.

  ```js
  // 적절한 모듈 및 클래스 이름
  // 고차원 개념, 알고리즘 정의
  // 모듈 및 클래스 정의
  // 저차원 함수 및 세부 내역
  ```

  고차원 함수 vs 저차원 함수

  > Low-level functions operate on the basic operations of a computer, such as bits and bytes. They are close to machine language and are often used in systems programming. On the other hand, high-level functions provide abstractions and handle complex operations. They are written in higher-level programming languages and are closer to human language, making them easier for humans to use. High-level functions can use low-level functions to implement their functionality, but the opposite is not always true.

- 빈 행으로 개념을 분리한다.

  ```js
  // import 문

  // 구현체
  ```

- 들여쓰기로 연관성을 나타낸다.
  ```js
  const Users = () => {
    const name = "";
    const age = "";
  };
  ```
- 간단한 if문, 짧은 while 문 등과 같이 들여쓰기를 무시할 수 있는 경우에도 들여쓰기를 사용하도록 한다.

  ```js
  // X
  if (isOpen) return <></>;

  // O
  if (isOpen) {
    return <></>;
  }
  ```

- 서로 밀접한 개념은 세로로 가까이 둔다.

  ```js
  const includeSetupPages = (isSuite) => {
    if (isSuite) includeSuiteSetupPage();
    includeSetupPage();
  };

  const includeSuiteSetupPage = () => {
    // …
  };
  ```

- 변수는 사용하는 위치에 최대한 가까이 선언한다.
  - 지역변수는 함수 맨 처음에 선언한다.
  - 루프 제어 변수는 루프 문 내에서 선언한다.
    ```js
    for(Test each: tests) {
        // ..
    }
    ```
- 가로 공백을 사용해 밀접한 개념과 느슨한 개념을 표현한다.
  - 변수 할당 시 공백을 주어 할당 연산자를 강조한다.
    ```
    let size = arr.length();
    ```
  - 함수이름과 이어지는 괄호는 밀접하므로 공백을 넣지 않는다.
  - 연산식에서 항 사이를 구분하기 위해 공백을 사용한다.
    ```
    (-num1 - num2) / 2*num3
    ```

* 가로정렬을 하지 않는다.
  <img width="731" alt="image" src="https://user-images.githubusercontent.com/67260437/217409523-c24a98d8-f1fa-4b11-8a18-40db1369b472.png">

  함수를 정의할 때 가로 정렬을 하는 경우 함수 이름보다 변수부터 보게되는 경향이 있다.
