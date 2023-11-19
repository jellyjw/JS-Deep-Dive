## 타입 변환이란?

JS의 모든 값에는 타입이 있는데, 개발자의 의도에 따라 다른 타입으로 변환될 수 있다. 이를 **명시적 타입 반환 또는 타입 캐스팅** 이라고 한다.

```jsx
let x = 10;
let string = x.toString();
console.log(typeof string); // string
```

개발자의 의도와 상관 없이 평가 도중 JS 엔진에 의해 암묵적으로 타입이 변환되기도 하는데, 이를 **암묵적 타입 변환 또는 타입 강제 변환** 이라고 한다.

```jsx
let x = 10;
let string = x + "";
console.log(typeof string); // number
```

두 경우 다 원시값을 직접 변경하는것은 아니다. 원시값은 변경 불가능한 immutable value 이므로 변경이 불가능하다. 타입 변환이란 기존 원시값을 사용해 다른 타입의 새로운 원시 값을 생성하는 것이다.

명시적 타입 반환의 경우 개발자의 의지가 드러나지만, 암묵적 타입 반환은 드러나지 않게 자동 변환되기 때문에 어떻게 평가될 것인지 예측 가능한 코드를 작성해야 한다.

**암묵적 타입 변환에서, 객체와 빈 배열이 아닌 배열, undefined는 변환되지 않아 `NaN` 이 된다는 것에 주의하자**

### false로 평가되는 Falsy 값

- false
- undefined
- null
- 0, -0
- NaN
- ‘’ (빈 문자열)

해당 값 이외의 모든 값은 모두 true로 평가되는 Truthy 값이다.

### 문자열 타입으로 변환하는 방법

- String 생성자 함수를 new 연산자 없이 호출
- Obejct.prototype.toString 메서드 사용
- 문자열 연결 연산자 이용

### 숫자 타입으로 변환

- Number 생성자 함수를 new 연산자 없이 호출
- parseInt, parseFloat 함수를 사용(문자열만 숫자 타입으로 변환 가능)
- - 단항 산술 연산자 이용
- - 산술 연산자 이용

### Boolean 타입으로 변환

- Boolean 생성자 함수를 new 연산자 없이 호출
- ! 부정 논리 연산자를 두 번 사용
  ```jsx
  !!0; // false
  !!1; // true
  !!NaN; // false
  ```

### 단축 평가

### 1) 논리 연산자를 사용한 단축 평가

논리합 또는 논리곱 연산자 표현식의 평과 결과는 불리언 값이 아닐수도 있다. **언제나 2개의 피연산자 중 어느 한쪽으로 평가된다.**

```jsx
"Cat" && "Dog"; // 'Dog'
```

논리곱 연산자는 두개의 피연산자가 모두 true일때 좌항에서 우항으로 평가가 진행되는데, **논리 연산의 결과를 결정하는 두 번째 피연산자, 즉 문자열 ‘Dog’ 을 그대로 반환한다.**

논리합 연산자(||) 도 동일하게 동작한다. **논리 연산의 결과를 결정한 첫 번째 피연산자, ‘Cat’ 을 그대로 반환**한다.

```jsx
"Cat" || "Dog"; // 'Cat'
```

이처럼, **논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환** 하는데 이를 **단축 평가**라고 한다.

단축 평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 **나머지 평가 과정을 생략** 하는 것을 말한다. 이런 단축 평가를 사용하면 if문을 대체할 수 있다.

1.1) 객체 변수가 null 또는 undefined 가 아닌지 확인하고 참조할 때

만약 특정 객체의 프로퍼티를 참조하고 싶은데, 해당 프로퍼티의 값이 `null` 이나 `undefined` 라면 타입 에러가 발생되며 프로그램이 종료된다. 이때 단축평가를 통해 에러를 발생시키지 않을 수 있다.

```jsx
let elem = null;
let value = elem.value; // TypeError

let value = elem && elem.value; // null
```

1.2) 함수 매개변수에 기본값 설정할 때

인수를 전달하지 않으면 매개변수에는 undefined가 할당된다. 이때 기본값을 단축평가를 사용해 설정하면 에러를 방지할 수 있다.

```jsx
function getStringLength(str) {
  str = str || "";
  return str.length;
}

getStringLength(); // 0
getStringLength("hi"); // 2
```

### 옵셔널 체이닝 연산자

ES11에서 도입된 옵셔널 체이닝 연산자 `?.` 는 좌항의 피연산자가 `null` 또는 `undefined` 일 경우 `undefined` 를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.

```jsx
let elem = null;

const value = elem?.value;
console.log(value); // undefined
```

논리연산자 &&는 좌항 피연산자가 false로 평가되는 Falsy 값이면 좌항 피연산자를 그대로 반환한다. 하지만 0이나 ‘’ 은 객체로 평가될 때도 있다.

하지만 옵셔널 체이닝 연산자는 좌항 피연산자가 false로 평가되는 Falsy 값이라도 `null` 또는 `undefined` 가 아니면 우항의 프로퍼티 참조를 이어간다.

```jsx
const str = "";
const length = str?.length;
console.log(length); // 0
```

### null 병합 연산자

ES11에서 도입된 null 병합 연산자 `??` 는 좌항의 피연산자가 null 또는 undefined 인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다. null 병합 연산자 ??는 변수에 기본값을 설정할 때 유용하다.

```jsx
const foo = null ?? "default string";
console.log(foo); // 'default string'
```

null 병합 연산자 도입 이전에는 논리연산자 || 를 사용한 단축 평가를 통해 기본값을 변수에 할당했다. 하지만 단축평가는 좌항의 피연산자가 Falsy 값이면 우항의 피연산자를 반환하는데 만약 0이나 ‘’ 도 기본값으로서 유효하다면 에러가 일어날수 있다.

```jsx
const foo = "" || "default string";
console.log(foo); // 'default string'
```

하지만 null 병합 연산자는, 좌항의 피연산자가 Falsy 값이라도 null이나 undefined 가 아니면 좌항의 피연산자를 그대로 반환한다.

```jsx
const foo = "" ?? "default string";
console.log(foo); // ''
```
