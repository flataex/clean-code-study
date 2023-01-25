### Q1. 다음 코드에서 "검색하기 쉬운 이름을 사용해라" 원칙을 위배한 부분을 찾으시오.

<pre>
    <code>
    {
        let sum = 0;
        for(let i = 1; i <= 10; i++){
            sum += i;
        };
        console.log(`sum : ${sum}`)
    }
    </code>
</pre>

<details>
  <summary>정답</summary>
  
  ### p.28
  for 문에 인자값으로 10이라는 상수가 있다. 10으로 검색하려면 여러가지 값이 나올것이고 이것을 옳지 않는 코딩이다.

  아래와 같이 MAX_SUM_NUMBER 변수를 추가해준다.

  ~~~
  {
        const MAX_SUM_NUMBER = 10;
        let sum = 0;
        for(let i = 1; i <= MAX_SUM_NUMBER; i++){
            sum += i;
        };
        console.log(`sum : ${sum}`)
  }
  ~~~

</details>


### Q2. 같은 종류에 함수에 fetch, retrieve, get 최대한 다양하게 이름을 지어야 보기가 좋다. ( O , X )

<details>
  <summary>정답</summary>
  
  ### p.33 X
  같은 종류의 함수는 한가지 이름으로 사용하는 것이 가독성이 높아진다.
</details>

### Q3. 함수는 길이가 작을수록 좋다. ( O , X )

<details>
  <summary>정답</summary>
  
  ### p.42 O
</details>


### Q4. 함수는 한가지 기능만 하는 함수여야한다. ( O , X )

<details>
  <summary>정답</summary>
  
  ### p.44 O
</details>

### Q5. 함수 인수는 많을수록 사용성이 증가하여 좋다. ( O , X )

<details>
  <summary>정답</summary>
  
  ### p.50 X
  함수 인자는 적을수록 가독성이 높아진다.
</details>

### Q6. 확장성을 고려하여 같은 코드여도 반복하여 사용한다. ( O , X )

<details>
  <summary>정답</summary>
  
  ### p.60 X
  같은 코드는 가능한 반복을 줄이는 것이 좋다.
</details>