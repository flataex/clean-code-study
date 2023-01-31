## 의미있는 이름

<br/>
<br/>

- 잘못된 정보를 제공하지 않는다.

```js
BalanceTableTitle, TradeTableTitle -> BalanceTableHeader, TradeTableHeader
```

```js
NoticeListTable, NoticeListItem ->
NoticeTable, NoticeItem
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
  - ProductData vs ProductInfo
  - Customer vs CustomerObject
  - StringName vs Name

<br/>

- 의미있는 맥락을 추가한다.

<br/>

- 다른 개념에 같은 단어 혹은 같은 개념에 다른 언어를 사용하지 않는다.
  - CookieManager, WebViewManager, ...
  - get-Api

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
