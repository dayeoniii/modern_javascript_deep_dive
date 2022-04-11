제 32장 String
=================
표준 빌트인 객체인 String은 원시 타입인 문자열을 다룰 때 유용한 프로퍼티와 메서드를 제공한다.   

32.1 String 생성자 함수
----------------------
표준 빌트인 객체인 String은 생성자 함수 객체다. (new 연산자로 인스턴스 생성 가능)   
String 생성자 함수에 인수를 전달하지 않고 new 연산자와 함께 호출하면 [[StringData]] 내부 슬롯에 빈 문자열을 할당한 String 래퍼 객체를 생성한다.
```javascript
const strObj = new String();
console.log(strObj);  //String {length: 0, [[PrimitiveValue]]: ""}
```
[[PrimitiveValue]]는 접근할 수 없는 프로퍼티다. 이는 [[StringData[[ 내부 슬롯을 가리킨다.

* String 래퍼 객체는 배열과 마찬가리조 length 프로퍼티와 인덱스를 나타내는 숫자 형식의 문자열을 프로퍼티 키로, 각 문자를 프로퍼티 값으로 갖는 유사 배열 객체이면서 이터러블이다.

32.2 length 프로퍼티
----------------------
length 프로퍼티는 문자열의 문자 개수를 반환한다.

32.3 String 메서드
----------------------
String 객체에는 원본 String 래퍼 객체를 직접 변경하는 메서드는 존재하지 않는다.   
즉, String 객체의 메서드는 언제나 새로운 문자열을 반환한다.   
문자열은 변경 불가능한 원시 값이기 때문에 String 래퍼 객체도 읽기 전용 객체로 제공된다.

### 32.3.1 String.prototype.indexOf   
대상 문자열에서 인수로 전달받은 문자열을 검색하여 첫번째 인덱스를 반환한다. (검색에 실패시 -1)   
ES6에서 도입된 String.prototype.includes 메서드를 사용하면 가독성이 더 좋다.   

### 32.3.2 String.prototype.search   
대상 문자열에서 인수로 전달받은 정규 표현식과 매치하는 문자열을 검색하여 일치하는 문자열의 인덱스를 반환한다. (검색에 실패시 -1)   

### 32.3.3 String.prototype.includes   
ES6에서 도입된 String.prototype.includes 메서드는 대상 문자열에 인수로 전달받은 문자열이 포함되어 있는지 확인하여 불리언 값을 반환한다.

### 32.3.4 String.prototype.startsWith   
대상 문자열이 인수로 전달받은 문자열로 시작하는지 확인하여 불리언 값을 반환한다.

### 32.3.5 String.prototype.endsWith   
대상 문자열이 인수로 전달받은 문자열로 끝나는지 확인하여 불리언 값을 반환한다.

### 32.3.6 String.prototype.charAt   
대상 문자열이 인수로 전달받은 인덱스에 위치한 문자를 검색하여 반환한다.

### 32.3.7 String.prototype.substring   
대상 문자열이 인수로 전달받은 문자열에서 첫번째 인수로 전달받은 인덱스에 위치하는 문자부터 두번째 인수로 전달받은 인덱스에 위치하는 문자의 바로 이전 문자까지의 부분 문자열을 반환한다.

### 32.3.8 String.prototype.slice   
slice 메서드는 substring 메서드와 동일하게 동작한다. 단, slice 메서드에는 음수인 인수를 전달할 수 있다.   
음수인 인수를 전달하면 대상 문자열의 가장 뒤에서부터 시작하여 문자열을 잘라내어 반환한다.

### 32.3.9 String.prototype.toUpperCase   
대상 문자열을 모두 대문자로 변경한 문자열을 반환한다.

### 32.3.10 String.prototype.toLowerCase   
대상 문자열을 모두 소문자로 변경한 문자열을 반환한다.
