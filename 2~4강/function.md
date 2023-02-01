# 3. 함수

## 작게 만들어라!

```
const setEmplyee = (emp) => {
  if (emp.dept === 'front-end'){
    emp.name = 'jamson';
    emp.phone = '01012345678';
  } else {
    emp.name = 'ballantines';
    emp.phone = '01056781234';
  }
  return emp;
}
```

위 코드는 emp를 분기처리하는 간단한 로직입니다. 하지만 옳지 않습니다.

```
const setEmplyee = (emp) => {
  if (emp.dept === 'front-end')
    return setFrontEnd(emp);

  return setOtherDept(emp);
}

const setFrontEnd = (emp) => {
  emp.name = 'jamson';
  emp.phone = '01012345678';
  return emp;
}

const setOtherDept = (emp) => {
  emp.name = 'ballantines';
  emp.phone = '01056781234';
  return emp;
}
```

- if문/else문/while문 등에 들어가는 내용은 한 줄로 줄여서 함수를 읽고 이해하기가 쉬워집니다.

## 한 가지만 해라!

- "함수는 한 가지를 해야 한다. 그 한 가지를 잘 해야 한다. 그 한 가지만을 해야 한다."

## 함수 당 추상화 수준은 하나로!

```
const Table = () => {
  const tableList = [...];

  return (
    tableList.map(item => <TableItem .../>)
  )
}

const TableItem = (...) => {
  return (
    <tr>
      <td>title</td>
      <td>contents</td>
    </trr>
  )
}

```

- 위에서 아래로 프로그램을 읽으면 함수 추상화 수준이 한 번에 한 단계씩 낮아지게 코딩해야합니다. (내려가기 규칙)

## Switch 문

- switch 문을 함수로 분리하여 숨기면서 SRP(Single-responsibility principle, 단일 책임 원칙)을 지킵니다.

```
const setColor = (e) => {
  switch (type) {
    case + :
    return 'red';
    case - :
    return 'blue';
    default:
    return 'gray';
  }
}
const CompoentA = () => {
  const color = setColor('+')

  return (
    <div color={color} />
  )
}

```

## 서술적인 이름을 사용

- "코드를 읽으면서 짐작했던 기능을 각 루틴이 그대로 수행한다면 깨끗한 코드라 불러도 되겠다."
- 길고 서술적인 이름이 짧고 어려운 이름보다 좋고 길고 서술적인 주석보다 좋습니다.
- 일관성있게 이름을 붙여야합니다. 문체가 비슷하면 이해하기가 쉬워집니다. (add, apend 등 혼용 금지)

## 함수 인수

- 함수에서 이상적인 인수 개수는 0개(무항)이며 적을수록 좋습니다.
- 플래그 인수는 사용하면 안됩니다.(하나의 함수는 한가지 일만 할것)
- 인수가 많아진다면 객체로 만들어 넘겨주는것도 좋습니다.

## 부수 효과를 일으키지 마라!

- 함수에서 한가지 기능만 작성하고 다른 기능을 추가하고 싶다면 함수 이름의 명시적으로 작성해야한다.

- 출력 인수
  - 함수의 인수로 받고 원본값을 변경하는것은 위험하기에 return하여 새로운 변수에 저장하거나 인수로 받는 변수를 class나 객체로 만들어 함수를 추가해주는것이 좋습니다.

```
const setColor = (color) => {
  color = 'red';
};

let color = 'blue';
setColor('blue');

// 객체로 만들어서 작업합니다.
class ColorObj {
    constructor(color) {
        this.color = color;
    }
    setColor(changeColor) {
      this.color = changeColor
    }
    console() {
        console.log(this.color)
    }
}
const color = new ColorObj('blue');

color.console();
color.setColor('red');
color.console();
```

## 명령과 조회를 분리하라

- 함수는 뭔가를 수행하거나 답을 return해야합니다. 두가지를 같이하는것을 옳지 않습니다.

```
if (set("username", "unclebob"))..
```

이 코드는 username 이라는 key에 unclebob를 set하는 것이 성공한 것인지 혹은 값이 맞는 비교하는 지 알기가 어렵습니다.

```
if (attributeExists("username")) {
  setAttribute("username", "unclebob");
}
```

## 오류 코드보다 예외를 사용하라!

- 오류 코드로 분기 처리하는 것보다 try/catch를 사용하여 하는것이 보기 좋으며 try 블록 안에 내용과 catch 블록 안에 내용은 별도의 함수로 분리하는것 좋습니다.

```
const delete = aync(Page page) =>{
  try {
    await deletePageAndAllReferences(page);
  }
  catch (Exception e) {
    logError(e);
  }
}

const deletePageAndAllReferences = (page) = >{
  ...
}

const logError = (e) => {
  logger.log(e.getMessage());
}
```

## 반복하지 마라!

## 구조적 프로그래밍

- 함수의 크기에 따라 큰 함수의 경우 return문은 하나로 해야 좋습니다. 하지만 작게 만든다면 return, break, continue를 사용해도 좋습니다.

## 함수는 어떻게 짜죠?

- 처음부터 완벽한 코드를 짜면 좋겠지만 숙력된다 하여도 쉽지 않습니다. 처음에 구현을 목표로 코드를 짜고 test code를 구현하고 중복되는 코드를 제거하고 분리할 수 있는 함수를 분리하고 컨벤션의 맞게 이름 지으면됩니다. 아 과정에서 test를 실패해서는 안됩니다.
