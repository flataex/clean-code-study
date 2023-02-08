# 7장 오류 처리

상당수 코드 기반은 전적으로 오류 처리 코드에 좌우되기 때문에 깨끗한 코드와 연관성이 있다.
* 여기저기 흩어진 오류 처리 코드 때문에 실제 코드가 하는 일을 파악하기가 어려워 질 수 있음.
* 오류 처리 코드로 인해 프로그램 논리를 이해하기 어려워진다면 깨끗한 코드라 부르기 어렵다.

1. 오류 코드보다 예외를 사용해라
에러코드를 사용하면 호출자 코드가 복잡해진다. 함수를 호출한 즉시 오류를 확인해야 하기 때문이다. 오류 처리를 잊기도 쉽다. 따라서 예외를 던지는 것이 낫다.
```javascript
// 오류 코드를 사용한 예시
const createUser = async (registrationData) => {
	const result = createUserApi(registrationData);
	if (result.status === ‘NETWORK_ERROR’) {
		console.error(“Network Error has occured”);
	} else if (result.stats === ‘WRONG_PARAMETER’) {
		console.error(“Wrong parameter incomed”);
	} else if …생략…
}

// 예외처리를 하는 경우
const createUser = async (registrationData) => {
	try {
		await createUserApi(registrationData);
	} catch(error) {
		console.error(error.message);
	}
}
```

2. Try-Catch-Finally 문부터 작성하라
	* try 블록에 들어가는 코드를 실행하면 어느 시점에서든 실행이 중단된 후 catch블록으로 넘어갈 수 있다.
	* try블록에서 무슨 일이 생기든지 catch블록은 프로그램 상태를 일관성 있게 유지해야 한다.
	* TDD(테스트 주도 개발)을 사용하면 자연스럽게 try블록부터 구현하게 되므로, 범위 내에서 트랜잭션 본질을 유지하기 쉬워진다.

3. 미확인 예외를 사용해라
	* 확인된 예외를 사용하게 되면 최하위에서 호출된 함수의 예외가 변경될 경우, 최상위의 함수들까지 예외에 대한 선언을 수정해야 한다.

4. 예외에 의미를 제공하라
	* 오류 메시지에 정보를 담아 예외와 함께 던진다.

5. 정상흐름을 정의하라
	* 클래스나 객체가 예외적인 상황을 캡슐화해 처리하여 클라이언트 코드가 예외적인 상황을 처리할 필요가 없도록 할 수 있다.
```javascript
try {
	…생략…
} catch(error) {
	// 잘못된 예시
	if(error.message === “MEAL_EXPENSES_NOT_FOUND”){
		total += getMealPerDay();
	}
}
```
	* 쉬운 말로, catch 문에서 추가 처리를 하기보다, try문에서 해결한다.

6. null을 반환하지 마라
	* 호출자에게 null 체크의 의무를 준다.
	* null 체크가 너무 많아진다.
	* 차라리 예외를 던지거나 특수사례 객체(ex.빈 객체)를 반환하는 것이 좋다.

#일상/공부
