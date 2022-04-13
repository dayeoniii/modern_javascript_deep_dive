제 39장 DOM
================
브라우저의 렌더링 엔진은 HTML 문서를 파싱하여 브라우저가 이해할 수 있는 자료구조인 DOM을 생성한다.   
DOM은 HTML 문서의 계층적 구조와 정보를 표현하여 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조다.

39.1 노드
---------------

### 39.1.1 HTML 요소와 노드 객체   
HTML 요소는 HTML 문서를 구성하는 개별적인 요소를 의미한다.   
<br/>
<p align="center">
<img src="./img/HTML 요소의 구조.PNG" width="65%" height="25%" align="center" title="HTML 요소의 구조" alt="HTML 요소의 구조"></img>
</p>
<br/>
HTML 요소는 렌더링 엔진에 의해 파싱되어 DOM을 구성하는 요소 노드 객체로 변환된다. 이때 HTML 요소의 어트리뷰트는 어트리뷰트 노드로, HTML 요소의 텍스트 콘텐츠는 텍스트 노드로 변환된다.
<br/>
<p align="center">
<img src="./img/HTML 요소와 노드 객체.PNG" width="50%" height="30%" align="center" title="HTML 요소와 노드 객체" alt="HTML 요소와 노드 객체"></img>
</p>

HTML 요소 간에는 중첩 관계에 의해 계층적인 부자 관계가 형성된다. 이러한 HTML 요소 간의 부자 관계를 반영하여 HTML 문서의 구성 요소인 HTML 요소를 객체화한 모든 노드 객체들을 트리 자료 구조로 구성한다.   

**트리 자료구조**   
트리 자료 구조는 노드들의 계층 구조로 이뤄진다. 즉, 트리 자료구조는 부모 노드와 자식 노드로 구성되어 노드 간의 계층적 구조를 표현하는 비선형 자료구조를 말한다. 노드 객체들로 구성된 트리 자료구조를 DOM이라 한다.

### 39.1.2 노드 객체의 타입   
DOM은 노드 객체의 계층적인 구조로 구성된다. 노드 객체는 종류가 있고 상속 구조를 갖는다.   
노드 객체에는 총 12개의 종류(노드 타입)이 있다. 이 중에서 중요한 노드 타입은 다음과 같이 4가지다.

**문서 노드 :**      
문서 노드는 DOM 트리의 최상위에 존재하는 루트 노드로서 document 객체를 가리킨다. document 객체는 브라우저가 렌더링한 HTML 문서 전체를 가리키는 객체로서 전역 객체 window의 document 프로퍼티에 바인딩되어 있다.   
브라우저 환경의 모든 자바스크립트 코드는 script 태그에 의해 분리되어 있어도 하나의 전역 객체 window를 공유한다. 즉, HTML 문서당 document 객체는 유일하다.   
문서 노드, 즉 document 객체는 DOM 트리의 루트 노드이므로 DOM 트리의 노드들에 접근하기 위한 진입점 역할을 담당한다.

**요소 노드 :**   
요소 노드는 HTML 요소를 가리키는 객체다. 요소 노드는 HTML 요소 간의 중첩에 의해 부자 관계를 가지며, 이 부자 관계를 통해 정보를 구조화한다. 따라서 요소 노드는 문서의 구조를 표현한다고 할 수 있다.

**어트리뷰트 노드 :**   
어트리뷰트 노드는 HTML 요소의 어트리뷰트를 가리키는 객체다. 어트리뷰트 노드는 어트리뷰트가 지정된 HTML 요소의 요소 노드와 연결되어 있다.   
어트리뷰트 노드는 부모 노드가 없으므로 요소 노드의 형제 노드는 아니다. 어트리뷰트 노드에 접근하여 어트리뷰트를 참조하거나 변경하려면 먼저 요소 노드에 접근해야 한다.

**텍스트 노드 :**   
텍스트 노드는 HTML 요소의 텍스트를 가리키는 객체다. 요소 노드가 문서의 구조를 표현한다면 텍스트 노드는 문서의 정보를 표현한다고 할 수 있다.   
텍스트 노드는 DOM 트리의 최종단이다. 따라서 텍스트 노드에 접근하려면 먼저 부모 노드인 요소 노드에 접근해야 한다.

### 39.1.3 노드 객체의 상속 구조   
DOM은 HTML 문서의 계층적 구조와 정보를 표현하며, 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조라고 했다.   
즉, DOM을 구성하는 노드 객체는 자신의 구조와 정보를 제어할 수 있는 DOM API를 사용할 수 있다.   
이를 통해 노드 객체는 자신의 부모, 형제, 자식을 탐색할 수 있으며, 자신의 어트리뷰트와 텍스트를 조작할 수도 있다.
<br/>
<p align="center">
<img src="./img/노드 객체의 상속 구조.PNG" width="65%" height="45%" align="center" title="노드 객체의 상속 구조" alt="노드 객체의 상속 구조"></img>
</p>

프로토타입 체인 관점에서 보자. input 요소를 파싱하여 객체화한 input 요소 노드 객체는 HTMLInputElement, HTMLElement, Element, Node, EventTarget, Object의 prototype에 바인딩되어 있는 프로토타입 객체를 상속받는다. 즉, input 요소 노드 객체는 프로토타입 체인에 있는 모든 프로토타입의 프로퍼티나 메서드를 상속받아 사용할 수 있다.
<p align="center">
<img src="./img/input 요소 노드 객체의 프로토타입 체인.PNG" width="26%" height="50%" align="center" title="input 요소 노드 객체의 프로토타입 체인" alt="input 요소 노드 객체의 프로토타입 체인"></img>
</p>

노드 객체는 공통된 기능일수록 프로토타입 체인의 상위에, 개별적인 고유 기능일수록 프로토타입 체인의 하위에 프로토타입 체인을 구축하여 노드 객체에 필요한 기능, 즉 프로퍼티와 메서드를 제공하는 상속 구조를 갖는다.

DOM은 HTML 문서의 계층적 구조와 정보를 표현하는 것은 물론 노드 객체의 종류, 즉 노드 타입에 따라 필요한 기능을 프로퍼티와 메서드의 집합인 DOM API로 제공한다. 이 DOM API를 통해 HTML의 구조나 내용 또는 스타일 등을 동적으로 조작할 수 있다.

39.2 요소 노드 취득
-------------------------
HTML의 구조나 내용 또는 스타일 등을 동적으로 조작하려면 먼저 요소 노드를 취득해야 한다.   
텍스트 노드는 요소 노드의 자식 노드이고, 어트리뷰터 노드는 요소 노드와 연결되어 있기 때문에 텍스트 노드나 어트리뷰트 노드를 조작하고자 할때도 마찬가지다.   
요소 노드의 취득은 HTML 요소를 조작하는 시작점이다. 이를 위해 DOM은 요소 노드를 취득할 수 있는 다양한 메서드를 제공한다.

### 39.2.1 id를 이용한 요소 노드 취득  
Document.prototype.getElementById 메서드는 인수로 전달한 id 어트리뷰트 값을 갖는 하나의 요소 노드를 탐색하여 반환한다.   
getElementById 메서드는 Document.prototype의 프로퍼티다. 따라서 반드시 문서 노드인 document를 통해 호출해야 한다.

### 39.2.2 태그 이름을 이용한 요소 노드 취득   
Document.prototype/Element.prototype.getElementsByTagName 메서드는 인수로 전달한 태그 이름을 갖는 모든 요소 노드들을 탐색하여 반환한다. 여러 개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체(유사 배열 객체이면서 이터러블)를 반환한다.

### 39.2.3 class를 이용한 요소 노드 취득   
Document.prototype/Element.prototype.getElementsByClassName 메서드는 인수로 전달한 class 어트리뷰트 값을 갖는 모든 요소 노드들을 탐색하여 반환한다. 인수로 전달할 class 값은 공백으로 구분하여 여러 개의 class를 지정할 수 있다. 여러 개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체(유사 배열 객체이면서 이터러블)를 반환한다.

### 39.2.4 CSS 선택자를 이용한 요소 노드 취득   
CSS 선택자는 스타일을 적용하고자 하는 HTML 요소를 특정할 때 사용하는 문법이다.   
Document.prototype/Element.prototype.querySelector 메서드는 인수로 전달한 CSS 선택자를 만족시키는 하나의 요소 노드를 탐색하여 반환한다.   
```javascript
/* id 선택자: id 값이 'foo'인 요소를 모두 선택 */
#foo { ... }
/* class 선택자: class 값이 'foo'인 요소를 모두 선택 */
.foo { ... }
```

### 39.2.5 특정 요소 노드를 취득할 수 있는지 확인   
Element.prototype.matches 메서드는 인수로 전달한 CSS 선택자를 토해 특정 요소 노드를 취득할 수 있는지 확인한다.   
이 메서드는 이벤트 위임을 사용할때 유용하다.

### 39.2.6 HTMLCollection과 NodeList   
DOM 컬렉션 객체인 HTMLCollection과 NodeList는 DOM API가 여러 개의 결과값을 반환하기 위한 DOM 컬렉션 객체다.   
HTMLCollection과 NodeList는 모두 유사 배열 객체이면서 이터러블이다. 따라서 for...of문으로 순회 가능하며 스프레드 문법을 사용하여 간단히 배열로 변환할 수 있다. 

**HTMLCollection :**   
getElementsByTagName, getElementsByClassName 메서드가 반환하는 HTMLCollection 객체는 노드 객체의 상태 변화를 실시간으로 반영하는 살아있는 DOM 컬렉션 객체다. 실시간으로 노드 객체의 상태 변경을 반영하여 요소를 제거할 수 있기 때문에 HTMLCollection 객체를 for문으로 순회하면서 노드 객체의 상태를 변경해야 할 때 주의해야 한다.

**NodeList :**    
HTMLCollection 객체의 부작용을 해결하기 위해 getElementsByTagName, getElementsByClassName 메서드 대신 querySelectorAll 메서드(NodeList 객체를 반환)를 사용하는 방법도 있다. NodeList 객체는 실시간으로 노드 객체의 상태 변경을 반영하지 않는 객체다.

노드 객체의 상태 변경과 상관없이 안전하게 DOM 컬렉션을 사용하려면 HTMLCollection이나 NodeList 객체를 배열로 변환하여 사용하는 것을 권장한다.
