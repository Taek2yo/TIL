# JavaScript 형변환(Type Casting)
> 자바스크립트는 동적 타입 언어로, 변수의 데이터 타입을 자동으로 변환하는 암시적 형 변환과 개발자가 의도적으로 데이터 타입을 변환하는 명시적 형 변환을 지원한다.

## 암시적 형 변환(Implicit type conversion)
> 암시적 형 변환은 자바스크립트 엔진이 필요에 따라 자동으로 데이터 타입을 변환하는 것. 명시적으로 변환을 지정하지 않고 연산자나 비교를 실행할 때 발생한다.

### 산술 연산자
> 덧셈 연산자 (+)는 숫자보다 문자열을 우선시하며, 숫자와 문자열이 결합할 경우 숫자를 문자열로 변환하여 연산.

```js
50 + 50; // 100 (number)
100 + "점"; // "100점" (string)
"100" + "점"; // "100점" (string)
"10" + false; // "10false" (string)
99 + true; // 100 (number)
```

### 다른 연산자(-, *, /, %)
> 덧셈 연산자와 달리 다른 산술 연산자(-, *, /, %)는 문자열로의 변환을 수행하지 않는다.

```js
"2" * false; // 0 (number)
2 * true; // 2 (number)
```

## 명시적 형 변환(Explicit Type Conversion)
> 명시적 형 변환은 개발자가 의도적으로 데이터 타입을 변환하는 것. 다양한 방법으로 데이터 타입을 변환할 수 있다.

### 숫자 타입으로 변환하기

#### Number()
> 문자열을 숫자로 변환하며, 변환할 수 없는 경우 NaN을 반환.
```js
Number("12345"); // 12345
Number("2" * 2); // 4
```

### 정수 타입으로 변환하기

#### parseInt()
> 문자열을 정수로 변환하며, 문자열이 숫자로 시작하지 않거나 빈 공백이 포함되어 있으면 변환이 실패하고 NaN을 반환.

```js
parseInt("27"); // 27
parseInt("0033"); // 27
parseInt("0x1b"); // 27
parseInt(" 2"); // 2
parseInt(" 2ㅎ"); // NaN
```

### 부동 소수점 타입으로 변환하기

#### parseFloat()
> 문자열을 부동 소수점 숫자로 변환하며, 문자열에 빈 공백이 포함되어 있으면 변환이 실패하고 NaN을 반환한다.
```js
parseFloat("123.123456"); // 123.123456
parseFloat(" 123.123456"); // 123.123456
parseFloat(" a123.123456"); // NaN
```

### 문자열 타입으로 변환하기
#### String()
> 값을 문자열로 변환.
```js
String(123); // "123"
String(123.456); // "123.456"
```

### 불린 타입으로 변환하기
#### Boolean()
> 값을 불린 타입으로 변환하며, 여러 값들은 true 또는 false로 변환.
```js
Boolean(100); // true
Boolean("1"); // true
Boolean(true); // true
Boolean(0); // false
Boolean(null); // false
Boolean(undefined); // false
```

### 단항 연산자를 사용한 숫자형 타입 변환
> 자바스크립트에서는 단항 연산자를 사용하여 숫자형 타입으로의 변환을 간편하게 수행할 수 있다.
```js
+'1000'; // 1000
+'-1000'; // -1000
+'Infinity'; // Infinity
-'1000'; // -1000
+true; // 1
+[]; // 0
+false; // 0
+null; // 0
+''; // 0
```

* 이 단항 연산자를 사용한 방법은 Number() 함수와 동일한 동작을 한다. 단항 연산자를 활용하면 간편하게 숫자형 타입으로 변환할 수 있다.

### A Type → String Type 다른 자료형을 문자열로 변환하는 방법

#### String()
```js
String(123); // "123"
String(123.456); // "123.456"
```

#### toString()
> toString() 메서드는 주어진 값을 문자열로 변환한 후 반환한다. 이 메서드를 사용할 때 기수(base)를 지정할 수 있으며, 기수를 지정하지 않으면 10진수로 변환한다.

```js
var trans = 100;
trans.toString(); // "100"
trans.toString(2); // "1100100"
trans.toString(8); // "144"

var boolT = true;
var boolF = false;
boolT.toString(); // "true"
boolF.toString(); // "false"
```

#### toFixed()
> toFixed() 메서드는 주어진 소수 자릿수만큼 반올림하여 소수점을 표현하고, 소수점 이하 자릿수가 넘치는 경우 '0'으로 길이를 맞춘 문자열을 반환한다.

```js
var trans = 123.456789;
var roundOff = 99.987654;
trans.toFixed(); // "123"
trans.toFixed(0); // "123"
trans.toFixed(2); // "123.46"
trans.toFixed(8); // "123.45678900"
roundOff.toFixed(2); // "99.99"
roundOff.toFixed(0); // "100"
```

### A Type → Boolean Type
> 자바스크립트에서는 Boolean 타입으로 변경할 때 Boolean() 함수나 부정 연산자 (!)를 사용한다. 부정 연산자를 사용하면 해당 값의 반대인 부울 값을 반환한다.

```js
Boolean()
Boolean(100); // true
Boolean("1"); // true
Boolean(true); // true
Boolean(Object); // true
Boolean([]); // true
Boolean(0); // false
Boolean(NaN); // false
Boolean(null); // false
Boolean(undefined); // false
Boolean(); // false

const numb1 = 0;
Boolean(numb1); // false
!!numb1; // false
!numb1; // true
```

* 위의 방법들을 사용하여 데이터 타입을 원하는 형태로 명시적으로 변환할 수 있다.

#### 참고
* MDN
* https://velog.io/@yejinh/Javascript-%ED%98%95%EB%B3%80%ED%99%98
* https://ko.javascript.info/type-conversions