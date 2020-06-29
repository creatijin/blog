### 객체타입

객체 타입은 속성을 포함하고 있으며, 호출 시그니처(call signature), 생성자 시그니처(construct signature) 등으로 구성

- Array

  배열 요소에 대응하며, 배열 안에 요소가 숫자 값이면 number[]가 타입이 된다.

  ~~~typescript
  let item:number[] = [1,2,3];
  ~~~

- Tuple

  배열 요소가 n개로 정해질 때 각 요소별로 타입을 지정하는 타입, 배열요소가 문자열과 숫자라면 [string, number]같은 형태로 타입 지정

  ~~~typescript
  let x:[string, number];
  x = ["tuple", 200];
  ~~~

- Function

  호출 시그니처에 포함되도록 정의된 타입 (6장에서 다룸)

- 생성자

  하나의 객체 (클래스로부터 생성)가 여러 생성자의 시그니처로 구성될 때 포함할 수 있는 타입, 생성자 타입 리터럴(constructor type literal) 사용하여 정의, 생성자 타입 리터럴은 생성자 시그니처를 구성하는 타입 매개변수, 매개변수 목록, 반환 타입으로 구성

  ~~~typescript
  new < 타입1,타입2, ... > (매개변수1, 매개변수2, ... ) => 타입
  ~~~

- Class,Interface

  객체 타입으로 분류되며, 객체지향 프로그래밍이나 구조 타이핑 등에 활용

### 기타타입

그 밖에 타입스크립트에서는 다음과 같은 타입을 지원한다.

- Union

  2개 이상의 타입을 하나의 타입으로 정의한 타입

  ~~~typescript
  var x: string | number;
  ~~~

- Intersection

  두 타입을 합쳐 하나로 만들 수 있는 타입

  ~~~typescript
  interface Cat {leg: number};
  interface Dog {bone: number};
  let catDog : Cat & Dog = {leg: 4, bone: 6};
  //catDog 변수가 인터섹션 타입인 Cat & Dog로 선언돼 있으므로 할당 객체는 leg, bone 속성만 허용
  ~~~

- 특수 타입

  타입 계층도의 가장 아래쪽에 위치한 void, null, undefined 가 있다. void는 빈 값을 나타내는 타입이다. 함수에 반환값이 없을 때 void 타입을 선언할 수 있는데 undefined나 null 값을 받을 때 사용함

  ~~~typescript
  function say(): void {
  	console.log("Hi");
  }
  let un: void = undefined;
  ~~~

  Void 타입은 반환값이 없을 때 빈번하게 사용되지만 변수에 undefined 나 null 값을 할당하는 경우는 흔치 않으므로 변수에 void 타입을 사용하는 것은 유용하지 않다.

  Undefined, null 타입은 다른 모든 타입의 하위 타입(subtype)이며, undefined는 어떠한 빈 값으로도 초기화되지 않는 타입이다.
  하지만 undefined와 다르게 null 타입은 빈 객체로 초기화 된다.

**타입스크립트의 타입 계층도는 기존 자바스크립트의 타입을 확장한 형태** 비교했을때 추가된 타입은

- 객체 타입의 상위 타입으로 any추가
- Any 타입의 특수 타입으로 유니언 타입과 인터섹션 타입 추가
- 객체(Object) 타입의 하위 타입으로 Array, Interface, Tuple 추가
- Void 타입 추가

### symbol 타입

Symbol 타입은 내장 타입 중 하나이며 ES6에 추가되었다. 특징으로는 객체 속성(Object property)의 유일하게 불변적인 식별자로 사용된다.

~~~javascript
let helloSym = Symbol("helloSym");
// Symbol함수를 이용하여 선언한다.
~~~

Symbol 함수는 심벌 객체를 반환 Symbol 함수가 유일한 식별자를 생성하는 팩토리 함수의 역활을 한다. Symbol함수를 호출할때 "helloSym" 인수는 심벌의 설명(description)을 의미한다. **설명은 심벌에 접근할 때 사용할 수 있으며, 생략도 가능하다.**

만약 변수를 불변 상수로 선언하려면 const 제한자를 이용해 변수를 선언한다.

~~~javascript
const hello - Symbol();
~~~

hello 변수는 유일하면서 (Symbol() 함수 사용) 불변(const 사용)이라는 특징을 지닌다.

~~~javascript
let sym = Symbol("sym1");
let sym2 = Symbol("sym2");
console.log(sym === sym2); // false
console.log(sym, sym2); // Symbol(sym1),Symbol(sym2)
console.log(typeof sym2); // symbol
~~~

위 결과로 보듯 심벌 객체는 호출될 때마다 새심벌 객체를 만든다 즉 유일한 심벌 객체가 만들어진다. (sym, sym2는 서로 다른 심벌 객체) 그리고 심벌 객체는 symbol 타입이라는 별도의 타입을 지닌다. 심벌 객체는 객체 리터럴의 속성 키로 사용할 수 있다.

~~~javascript
const uni = Symbol();
let obj = {};
obj[uni] = 1234;
console.log(obj[uni]); // 1234
console.log(obj); // {[Symbol()]:1234}
~~~

obj의 출력 결과가 빈객체인 이유는 uni 심벌 키는 충돌을 피할 목적으로 생성했으므로 객체에서 심벌키는 무시돼서 출력되기 때문이다. Symbol() 함수의 반환값은 별다른 값을 취하지 않아도 그 자체로 식별자가 된다.

### enum 타입

