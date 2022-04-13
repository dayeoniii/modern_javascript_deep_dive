제 37장 Set과 Map
==================

37.1 Set
------------------
Set 객체는 중복되지 않는 유일한 값들의 집합이다. Set 객체는 배열과 유사하지만 다음과 같은 차이가 있다.
<br/>
<p align="center">
<img src="./img/Set과 배열 차이.PNG" width="60%" height="18%" align="center" title="Set과 배열 차이" alt="Set과 배열 차이"></img>
</p>
<br/>
Set 객체의 특성은 수학적 집합의 특성과 일치한다. (수학적 집합을 구현하기 위한 자료구조)

### 37.1.1 Set 객체의 생성   
Set 객체는 Set 생성자 함수로 생성한다. 인수를 전달하지 않으면 빈 Set 객체가 생성된다.
Set 생성자 함수는 이터러블을 인수로 전달받아 Set 객체를 생성한다. 이때 이터러블의 중복된 값은 Set 객체에 요소로 저장되지 않는다.
```javascript
const set1 = new Set([1, 2, 3, 3]);
console.log(set1); // Set(3) {1, 2, 3}

const set2 = new Set('hello');
console.log(set2) // Set(4) {"h", "e", "l", "o" }
```
중복을 허용하지 않는 특성을 활용해 배열에서 중복된 요소 제거 가능

### 37.1.2 요소 개수 확인   
Set 객체의 요소 개수를 확인할 때는 Set.prototype.size 프로퍼티를 사용한다.
```javascript
const { size } = new Set([1, 2, 3, 3]);
console.log(size) // 3
```
size 프로퍼티는 setter 함수 없이 getter 함수만 존재하는 접근자 프로퍼티다. 따라서 size 프로퍼티에 숫자를 할당하여 객체 요소 개수 변경 불가.

### 37.1.3 요소 추가   
Set 객체에 요소를 추가할 때는 Set.prototype.add 메서드를 사용한다.
```javascript
const set = new Set();
console.log(set); // Set(0) {}

set.add(1);
console.log(set); // Set(1) {1}
```
add 메서드는 새로운 요소가 추가된 Set 객체를 반환한다.

### 37.1.4 요소 존재 여부 확인   
Set 객체에 특정 요소가 존재하는지 확인하려면 Set.prototype.has 메서드를 사용한다. 존재 여부를 불리언 값으로 반환한다.
```javascript
const set = new Set([1, 2, 3])
console.log(set.has(2)); //true
```

### 37.1.5 요소 삭제   
Set 객체의 특정 요소를 삭제하려면 Set.prototype.delete 메서드를 사용한다. 삭제 성공여부를 불리언 값으로 반환한다.   
delete 메서드에는 인덱스가 아니라 삭제하려는 요소값을 인수로 전달해야 한다. Set 객체는 순서에 의미가 없다.(배열과 같이 인덱스를 갖지 않음)
```javascript
const Set = new Set([1, 2, 3]);

// 요소 2를 삭제한다.
set.delete(2);
console.log(set); // Set(2) {1, 3}
```

### 37.1.6 요소 일괄 삭제   
Set 객체의 모든 요소를 일괄 삭제하려면 Set.prototype.clear 메서드를 사용한다. clear 메서드는 언제나 undefined를 반환한다.   
```javascript
const set = new Set([1, 2, 3]);

set.clear();
console.log(set); // Set(0) {}
```

### 37.1.7 요소 순회   
Set 객체의 요소를 순회하려면 Set.prototype.forEach 메서드를 사용한다.   
Set.prototype.forEach 메서드는 Array.prototype.forEach와 유사하게 콜백 함수와 forEach 메서드의 콜백 함수 내부에서 this로 사용될 객체를 인수로 전달한다. 콜백 함수는 다음과 같이 3개의 인수를 전달받는다.
1. 첫번째 인수 : 현재 순회 중인 요소값
2. 두번째 인수 : 현재 순회 중인 요소값 (Set 객체는 순서에 의미가 없어 인덱스를 갖지 않음)
3. 세번째 인수 : 현재 순회 중인 Set 객체 자체

* Set 객체는 이터러블이다. 따라서 for ... of문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링의 대상이 될 수도 있다.

### 37.1.8 집합 연산   
Set 객체를 통해 교집합, 합집합, 차집합 등을 구현할 수 있다.

37.2 Map
------------
Map 객체는 키와 값의 쌍으로 이루어진 컬렉션이다. Map 객체는 객체와 유사하지만 다음과 같은 차이가 있다.
<br/>
<p align="center">
<img src="./img/Map과 객체 차이.PNG" width="60%" height="18%" align="center" title="Map과 객체 차이" alt="Map과 객체 차이"></img>
</p>

### 37.2.1 Map   
Map 객체는 Map 생성자 함수로 생성한다. 인수를 전달하지 않으면 빈 Map 객체가 생성된다.   
Map 생성자 함수는 이터러블을 인수로 전달받아 Map 객체를 생성한다. 이때 인수로 전달되는 이터러블은 키와 값의 쌍으로 이루어진 요소로 구성되어야 한다.   
```javascript
const map1 = new Map([['key1', 'value1'], ['key2', 'value2']]);
console.log(map1); //Map(2) => {"key1" => "value1", "key2" => "value2"}   

const map2 = new Map([1, 2]); //TypeError: Iterator value 1 is not an entry object
```
Map 생성자 함수의 인수로 전달한 이터러블에 중복된 키를 갖는 요소가 존재하면 값이 덮어써진다. (Map 객체에는 중복된 키를 갖는 요소가 존재할 수 없다)

### 37.2.2 요소 개수 확인   
Map 객체의 요소 개수를 확인할 때는 Map.prototype.size 프로퍼티를 사용한다.   
ize 프로퍼티는 setter 함수 없이 getter 함수만 존재하는 접근자 프로퍼티다. 따라서 size 프로퍼티에 숫자를 할당하여 객체 요소 개수 변경 불가.

### 37.2.3 요소 추가   
Map 객체에 요소를 추가할 때는 Map.prototype.set 메서드를 사용한다.   
```javascript
const map1 = new Map();
console.log(map);  // Map(0) {}

map.set('key1', 'value1');
console.log(map); // Map(1) {"key1" => "value1"}
```
set 메서드는 새로운 요소가 추가된 Map 객체를 반환한다. 따라서 set 메서드를 호출한 후에 set 메서드를 연속적으로 호출할 수 있다.   
중복된 키를 갖는 요소를 추가하면 값이 덮어써진다.   

### 37.2.4 요소 취득   
Map 객체에서 특정 요소를 취득하려면 Map.prototype.get 메서드를 사용한다.   
get 메서드의 인수로 키를 전달하면 Map 객체에서 인수로 전달한 키를 갖는 값을 반환한다. (전달한 키를 갖는 요소가 없으면 undefined 반환)   

### 37.2.5 요소 존재 여부 확인   
Map 객체에 특정 요소가 존재하는지 확인하려면 Map.prototype.has 메서드를 사용한다.   
has 메서드는 특정 요소의 존재 여부를 나타내는 불리언 값을 반환한다.

### 37.2.6 요소 삭제   
Map 객체의 요소를 삭제하려면 Map.prototype.delete 메서드를 사용한다. 삭제 성공 여부를 나타내는 불리언 값을 반환한다.

### 37.2.7 요소 일괄 삭제   
Map 객체의 요소를 일괄 삭제하려면 Map.prototype.clear 메서드를 사용한다. clear 메서드는 언제나 undefined를 반환한다.   

### 37.2.8 요소 순회   
Map 객체의 요소를 순회하려면 Map.prototype.forEach 메서드를 사용한다.   
Map.prototype.forEach 메서드는 Array.prototype.forEach와 유사하게 콜백 함수와 forEach 메서드의 콜백 함수 내부에서 this로 사용될 객체(옵션)를 인수로 전달한다. 콜백 함수는 다음과 같이 3개의 인수를 전달받는다.
1. 첫번째 인수 : 현재 순회 중인 요소값
2. 두번째 인수 : 현재 순회 중인 요소키
3. 세번째 인수 : 현재 순회 중인 Map 객체 자체

* Map 객체는 이터러블이다. 따라서 for ... of문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링의 대상이 될 수도 있다.   
Map 객체는 이터러블이면서 동시에 이터레이터인 객체를 반환하는 메서드를 제공한다.
<br/>
<p align="center">
<img src="./img/Map 메서드.PNG" width="60%" height="18%" align="center" title="Map 메서드" alt="Map 메서드"></img>
</p>
<br/>
