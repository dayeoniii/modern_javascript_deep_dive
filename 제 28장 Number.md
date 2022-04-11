제 28장 Number
==================
표준 빌트인 객체인 Number는 원시 타입인 숫자를 다룰 때 유용한 프로퍼티와 메서드를 제공한다.   

28.1 Number 생성자 함수
----------------------------
표준 빌트인 객체인 Number 객체는 생성자 함수 객체다. 따라서 new 연산자와 함께 호출하여 Number 인스턴스를 생성할 수 있다.   
Number 생성자 함수에 인수를 전달하지 않고 new 연산자와 함께 호출하면 [[NumberData]] 내부 슬롯에 0을 할당한 Number 래퍼 객체를 생성한다.
```javascript
const numObj = new Number();
console.log(numObj);  //Number {[[PrimitiveValue]]: 0}

const numObj2 = new Number(10);
console.log(numObj2) // Number {[[PrimitiveValue]]: 10}

```

* Number 생성자 함수의 인수로 숫자가 아닌 값을 전달하면 인수를 숫자로 강제 변환한 후, [[NumberData]] 내부 슬롯에 변환된 숫자를 할당한 Number 래퍼 객체를 생성한다.   
인수를 숫자로 변환할 수 없다면 NaN을 [[NumberData]] 내부 슬롯에 할당한 Number 래퍼 객체를 생성한다. 

* new 연산자를 사용하지 않고 Number 생성자 함수를 호출하면 Number 인스턴스가 아닌 숫자를 반환한다.
```javascript
//문자열 타입 => 숫자 타입
Number('0');  // -> 0
Number('-1'); // -> -1
Number('10.53'); // -> 10.53

//불리언 타입 => 숫자 타입
Number(true); // -> 1
Number(false); // -> 0
```

28.2 Number 프로퍼티   
--------------------------
### 28.2.1 Number.EPSILON   
Number.EPSILON은 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이와 같다. (부동소수점으로 인해 발생하는 오차를 해결하기 위해 사용함)   

### 28.2.2 Number.MAX_VALUE   
Number.MAX_VALUE는 자바스크립트에서 표현할 수 있는 가장 큰 양수 값이다. Number.MAX_VALUE보다 큰 숫자는 Infinity다.

### 28.2.3 Number.MIN_VALUE   
Number.MIN_VALUE는 자바스크립트에서 표현할 수 있는 가장 작은 양수값이다. Number.MIN_VALUE보다 작은 숫자는 0이다.

### 28.2.4 Number.MAX_SAFE_INTEGER   
Number.MAX_SAFE_INTEGER는 자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수값이다.

### 28.2.5 Number.MIN_SAFE_INTEGER   
Number.MIN_SAFE_INTEGER는 자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수값이다.

### 28.2.6 Number.POSITIVE_INFINITY   
Number.POSITIVE_INFINITY는 양의 무한대를 나타내는 숫자값 Infinity와 같다.

### 28.2.7 Number.NEGATIVE_INFINITY   
Number.NEGATIVE_INFINITY는 음의 무한대를 나타내는 숫자값 -Infinity와 같다.  

### 28.2.8 Number.NaN   
Number.NaN은 숫자가 아님을 나타내는 숫자 값이다. Number.NaN이다. window.NaN과 같다.

28.3 Number 메서드
----------------------
### 28.3.1 Number.isFinite   
ES6에서 도입된 Number.isFinite 정적 메서드는 인수로 전달된 숫자값이 정상적인 유한수, 즉 Infinity 또는 -Infinity가 아닌지 검사하여 불리언 값으로 반환한다. (인수가 NaN이면 false 반환)

### 28.3.2 Number.isInteger   
ES6에서 도입된 Number.isInteger 정적 메서드는 인수로 전달된 숫자값이 정수인지 검사하여 불리언 값으로 반환한다.   
검사하기 전에 인수를 숫자로 암묵적 타입 변환하지 않는다. 

### 28.3.3 Number.isNaN   
ES6에서 도입된 Number.isNaN 정적 메서드는 인수로 전달된 숫자값이 NaN인지 검사하여 불리언 값으로 반환한다.   
검사하기 전에 인수를 숫자로 암묵적 타입 변환하지 않는다.

### 28.3.4 Number.isSafeInteger   
ES6에서 도입된 Number.isSafeInteger 정적 메서드는 인수로 전달된 숫자값이 안전한 정수인지 검사하여 불리언 값으로 반환한다.   
검사하기 전에 인수를 숫자로 암묵적 타입 변환하지 않는다. 

### 28.3.5 Number.toExponential   
toExponential 메서드는 숫자를 지수 표기법으로 변환하여 문자열로 반환한다.   
지수 표기법이란 매우 크거나 작은 숫자를 표기할 때 주로 사용하여 e 앞에 있는 숫자에 10의 n승을 곱하는 형식으로 수를 나타내는 방식이다.

### 28.3.6 Number.toFixed   
toFixed 메서드는 숫자를 반올림하여 문자열로 반환한다.   
반올림하는 소수점 이하 자릿수를 나타내는 0 ~ 20 사이의 정수값을 인수로 전달할 수 있다.(생략하면 0)

### 28.3.7 Number.toPrecision   
toPrecision 메서드는 인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환한다.   
인수로 전달받은 전체 자릿수로 표현할 수 없는 경우 지수 표기법으로 결과를 반환한다.

### 28.3.8 Number.toString   
toString 메서드는 숫자를 문자열로 변환하여 반환한다. 진법을 나타내는 2 ~ 36 사이의 정수값을 인수로 전달할 수 있다.(생략하면 10진법)

