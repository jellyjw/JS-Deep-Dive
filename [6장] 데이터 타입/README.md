데이터 타입은 값의 종류를 말한다. 자바스크립트의 모든 값은 **데이터 타입** 을 갖는다.

JS (ES6) 는 7개의 데이터 타입을 제공한다. 7개의 데이터 타입은 원시타입과 객체타입으로 분류할수 있다.

## 원시타입

| 데이터 타입      | 종류     | 설명                                                                                       |
| ---------------- | -------- | ------------------------------------------------------------------------------------------ |
| 문자열 (String)  | 원시타입 | 텍스트 데이터를 나타내며, String 객체로 변환 가능                                          |
| 숫자 (Number)    | 원시타입 | 숫자 데이터를 나타내며, Number 객체로 변환 가능                                            |
| 불리언 (Boolean) | 원시타입 | 논리적 참(True) 또는 거짓(False)을 표현                                                    |
| undefined        | 원시타입 | 값이 할당되지 않았거나 변수에 없는 경우, var 키워드로 선언된 변수에 암묵적으로 할당되는 값 |
| null             | 원시타입 | 값이 없다는 것을 의도적으로 명시할때 사용하는 값                                           |
| Symbol           | 원시타입 | 고유하고 변경불가능한 식별자를 나타냄. ES6에서 추가된 7번째 타입                           |
| BigInt           | 원시타입 | 큰 정수를 나타내며, BigInt 객체로 변환 가능                                                |

## 객체타입

- 객체, 함수, 배열 등

---

### 숫자(Number)

JS에는 하나의 숫자 타입만이 존재한다. 배정밀도 64비트 부동소수점 형식을 따르기 때문에, 모든 수를 실수로 처리하며 정수만 표기하기 위한 데이터 타입이 별도로 존재하지 않는다.

즉, 이는 정수로 표시된다 해도 사실은 **실수** 라는 것을 의미하며 정수로 표시되는 수끼리 나누더라도 실수가 나올수 있다.

```jsx
console.log(1 === 1.0); // true
```

숫자 타입은 3가지의 특별한 값도 표현할수 있다.

- Infinity : 양의 무한대
- -Infinity : 음의 무한대
- NaN : 산술 연산 불가 (Not-a-number)

### 문자열

문자열은 텍스트 데이터를 나타내는데 사용되며, 일반적으로 `''` , `""` , 백틱(``) 을 사용해 표기한다.

문자열을 따옴표나 백틱으로 감싸지 않으면 키워드나 식별자 같은 토큰으로 인식한다. JS의 문자열은 immutable value로 변경 불가능한 값인데, 문자열이 생성되면 변경이 불가능하다는 것을 의미한다.

### 템플릿 리터럴

ES6부터 추가된 템플릿 리터럴은 백틱(``) 을 사용해 표현하는 것으로, 다음과 같은 특징이 있다.

- 멀티라인 문자열
  - 일반 문자열에서는 줄바꿈 등의 공백을 표현하려면 백슬래시로 시작하는 이스케이프 시퀀스를 사용해야 한다.
  - ex) `\r` 줄바꿈, `\t` 탭(수평) 등…
  - 하지만 템플릿 리터럴은 줄바꿈, 공백을 모두 허용하며 입력한 문자열 있는 그대로 적용된다.
- 표현식 삽입
  - 일반 문자열에서는 문자열을 연결할때 `+` 연산자를 사용해서 연결했다.
  - 템플릿 리터럴은 `${}` 으로 표현식을 감싸서 간단히 삽입할수 있고, 평가 결과가 문자열이 아니더라도 문자열로 강제로 변환되어 삽입된다.

```jsx
const name = "jelly";
const msg = `${name}님께 메세지가 도착했어요.`; // 'jelly님께 메세지가 도착했어요.'
```

### 불리언(Boolean)

불리언 타입은 논리적 참, 거짓을 나타내는 `true` 와 `false` 뿐이다.

### undefined

값은 undefined 가 유일하다. `var` 키워드로 선언한 변수는 JS 엔진에 의해 암묵적으로 `undefined` 로 초기화된다.

따라서 변수를 선언한 이후 값을 할당하지 않으면 `undefined` 를 반환한다.

```jsx
var x;
console.log(x); // undefined
```

JS 엔진이 초기화할때 암묵적으로 할당하는 값이므로, 개발자가 의도적으로 변수에 할당한다면 혼란을 줄 수 있다.

만약 값이 없을때는 `null` 을 할당하는것이 좋다.

### null

값은 null 이 유일하다. `null` 은 값이 없다는 것을 의도적으로 명시할때 사용하며 변수에 `null` 을 할당하는 것은 더이상 이전에 참조하던 값을 참조하지 않겠다는 의미이다.

이는 이전에 할당되어 있던 값에 대한 참조를 명시적으로 제거하는 것을 의미하며, JS 엔진은 참조되지 않는 메모리 공간에 대해 가비지 콜렉션을 수행한다.

함수가 유효한 값을 반환할 수 없는 경우 명시적으로 `null` 을 반환하기도 한다.

```jsx
var element = document.querySelector("#myId");
// 해당 element 요소가 없다면 null을 반환
console.log(element); // null
```

### Symbol

ES6에서 추가된 7번째 타입으로, 변경 불가능한 원시타입의 값이다. 다른 값과 중복되지 않는 유일무이한 값이기 때문에 주로 이름이 충돌할 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용한다.

다른 원시값은 리터럴을 통해 생성하지만, 심벌은 `symbol` 함수를 호출해 생성한다. 이때 생성된 심벌값은 외부에 노출되지 않으며 다른 값과 절대 중복되지 않는다.

```jsx
const key = symbol("key");
console.log(typeof key); // 'symbol'
```

### 객체(Object)

JS의 타입은 크게 원시타입과 객체타입으로 구분되는데, 11장에서 자세히 살펴보겠다.

중요한 것은 JS는 객체 기반의 언어로 **거의 모든 것이 객체**로 이루어져 있다는 것이다.

### 데이터 타입의 필요성

**1) 데이터 타입에 의한 메모리 공간의 확보와 참조**

값은 메모리에 저장하고, 참조할수 있어야 한다. 저장하려면 확보해야 할 메모리의 공간 크기를 결정해야 한다.

JS 엔진은 데이터 타입, 즉 값의 종류에 따라 메모리 공간을 확보한다.

**2) 데이터 타입에 의한 값의 해석**

메모리에서 읽어 들인 2진수를 어떻게 해석할까? 모든 값은 데이터 타입을 가지며 2진수, 즉 비트의 나열로 저장된다.

문자열로 해석하느냐, 숫자로 해석하느냐에 따라 값이 달라질수 있다.

정리하자면 다음과 같다.

- 값을 저장할때 확보해야 하는 **메모리 공간의 크기** 를 결정하기 위해
- 값을 참조할때 한번에 읽어 들여야 할 **메모리 공간의 크기**를 결정하기 위해
- 메모리에서 읽어 들인 **2진수를 어떻게 해석** 할지 결정하기 위해

### 동적 타이핑

C나 자바같은 정적 타입 언어는 변수의 타입을 변경할수 없고, 지정한 타입에 맞는 값만 할당할수 있다. 만약 컴파일 시점에 타입 체크를 통과하지 못하면 에러를 발생시켜 프로그램의 실행 자체를 막아 더욱 안정적인 코드를 구현할수 있다.

하지만 자바스크립트는 **동적 타입 언어** 이다. 변수를 선언할때 타입을 선언하지 않고, 어떠한 데이터 타입의 값이라도 자유롭게 할당할수 있다.

JS의 변수는 **선언이 아닌 할당에 의해 타입이 결정(타입 추론)된다. 그리고 재할당에 의해 변수의 타입이 동적으로 변할수 있다.**

따라서 이런 동적 타입 언어는 **유연성** 은 높지만 **신뢰성** 은 떨어진다는 특징이 있다.

- 변수는 꼭 필요한 경우에 한해 제한적으로 사용하자.
- 변수의 유효 범위(스코프)를 최대한 좁게 만들어 변수의 부작용을 억제하자.
- 전역변수는 최대한 사용하지 않도록 하자.
- 변수보다는 상수를 사용해 값의 변경을 억제하자.
- 변수 이름은 목적이나 의미에 맞게 신중하게 짓자.
