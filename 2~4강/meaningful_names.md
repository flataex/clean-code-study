## 의미있는 이름

<br/>
클린코드 제 2장을 참고하여 기존 프로젝트에서 책에서 말하고 있는 <strong>의미있는 이름</strong>에 부합하거나 부합되지 않는다고 생각되는 부분을 일부 정리하였습니다.

<br/>

아래 내용을 참고하여 리팩토링 시 개선시켜야 할 점들을 더 찾아보고 개선시키도록 하는 것이 좋을 것 같습니다!
<br/>
<br/>
<br/>

- 잘못된 정보를 제공하지 않는다.

널리 쓰이는 의미가 있는 단어를 다른 의미로 사용하지 않도록 한다.

<img width="272" alt="tableEx" src="https://user-images.githubusercontent.com/67260437/215921027-8c880f10-8154-4f56-85e0-fbee1e310c1a.png">

`-TableTitle`로 생성한 컴포넌트가 table header의 기능을 하고 있다.

```js
BalanceTableTitle, TradeTableTitle -> BalanceTableHeader, TradeTableHeader
```

`List`와 같은 컨테이너 유형은 이름에 넣지 않는 것이 바람직하다.

```js
NoticeListTable, NoticeListItem -> NoticeTable, NoticeItem
```

<br/>

- 서로 흡사한 이름을 사용하지 않는다.

```js
// market/selector

MarketListDataState; // Tab
MarketListState; // name, coin type filter
```

<br/>

- 검색에 용이하도록 상수와 변수명을 사용한다.

```js
await api({
  method: "POST",
  url: "/confirmPasswordFindAuth",
  data: {
    ...data,
    pswdLevel: 3,
  },
});
```

```js
// e 대신 변수명을 부여한다.
<Atoms.TextInput onChange={(e) => setOtpNo(e.target.value)} />
```

<br/>

- `Data`, `Info`, `variable`, `String`와 같은 noise word는 특정한 이유가 없는 한 지양한다.  
  다음 예시와 같이 nosie word를 충분한 이유 없이 붙여 사용할 경우 두 개념의 차이를 명확히 이해하기 어렵다.
  - Product vs ProductInfo
  - Customer vs CustomerObject
  - StringName vs Name

<br/>

- method는 동사(구)를 사용한다. (`get`, `set`, `is`, ..)

```js
// 동사로 수정 필요
export const nearElement = (arr: Array<any>, target: any): any => {};
```

<br/>

- 클래스와 객체 이름은 명사(구)가 적합하다.

```js
export const Lv4InfoState = selector({});

export const LoginListState = selector({});

// 명사로 수정 필요
export const GetBankAccountState = selector({});
```

<br/>

- 의미있는 맥락을 추가한다.

  - 접두어를 활용하여 유사한 개념을 가진 변수간에 통합성을 준다.
  - 함수를 쪼개 변수가 어떻게 사용되는지 먼저 보여주는 맥락으로 개발한다.

<br/>

- 다른 개념에 같은 단어 혹은 같은 개념에 다른 언어를 사용하지 않는다.
  - CookieManager, WebViewManager, ...
  - get-Api
