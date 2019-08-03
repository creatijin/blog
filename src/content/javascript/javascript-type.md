---
layout: post
title: "타입"
author: Creatijin
tags: ["javascript"]
image: ../img/javascript-posting-type.jpg
date: "2019-08-04T04:47:00.000Z"
draft: false
---
# 타입

##1.내장 타입

자바스크립트에는 7가지 내장 타입이 존재한다.

- null
- undefined
- boolean
- number
- string
- object
- symbol(ES6부터 추가)

**object를 제외하고 원시타입(primitives)이라 한다.**



Typeof 연산자로 값의 타입을 알 수 있다.

~~~javascript
typeof undefined === 'undefined'; //true
typeof true === 'boolean'; //true
typeof 92 === 'number'; //true
typeof "92" === 'string'; //true
typeof { life: 92 } === 'object' //true

//ES6부터 추가
typeof  Symbol() === 'symbol'; //true

//???
typeof null === 'object'; //true
~~~

위 결과를 보면 typeof의 반환 값이 7가지 내장 타입과 1:1로 정확히 매치되지 않는다. 6개 타입(null을 제외한)은 자신의 명칭과 동일한 문자열을 반환한다, 하지만 null의 반환 값은 명칭과 동일하지 않는다.

**null을 반환해야하는게 맞다** 이 오류는 자바스크립트에 20년 동안 존재했으며 지금으로써는 해결하기 힘든 버그로 자리잡았다. (버그를 수정할 경우 그동안 잘 돌아가던 웹 소프트웨어가 문제가 생길지 모르기 때문이다)



null 값의 타입을 좀 더 정확히 확인 해야한다면 조건을 더 추가해야한다.

~~~~javascript
var a = null;
(!a && typeof a === "object"); //true
//a가 false임을 확인하고 다음 조건인 typeof를 확인
~~~~

null은 **'falsy'[^1]**한 유일한 원시 값이지만 타입은 object인 특별한 존재다.

[^1]:true/false를 일일이 참/거짓으로 옮기지 않고, '불리언 문맥 상 true/false로 봐야하는 값'으로 이해



typeof가 반환하는 문자열이 하나 더 있다.

~~~javascript
typeof function a() {} === 'function'; //true
~~~

자바스크립트에서 함수는 객체이다, 실제로는 object의 하위 타입, 다시 말해  **함수는 '호출 가능한 객체'**다.

함수는 다른 객체처럼 속성 및 메서드를 가질 수 있기 때문에 **일급 객체**라 불린다. 더 자세한 내용은 [Javascript - Function](https://creatijin.netlify.com/basic/함수/) 를 참조하자.

함수는 객체이기 때문에 유용한 점이 있다. 그중에 하나는 프로퍼티를 가질 수 있다. 그리고 인자 개수는 함수 객체의 Length 프로퍼티로 알 수 있다.

~~~~javascript
function c(a,b) {}

c.length; // 2
// c 함수는 인자를 가지므로 length 프로퍼티로 2를 알 수 있다.
~~~~

함수도 확인했으니 자바스크립트의 중요한 배열도 확인해 보자

~~~javascript
typeof [1,2,3] === 'object'; //true
~~~

배열 또한 객체이다. 객체의 하위 타입으로써 숫자 인덱스를 가지며, length 프로퍼티가 자동으로 관리 되는 등 추가 특성을 지닌다.



## 2.값은 타입을 가진다

자바스크립트는 값에는 타입이 존재한다, 하지만 변수(variable)에는 타입이 존재하지 않는다. 그러기에 변수는 어떠한 형태의 값이라도 가질 수 있다.

자바스크립트는 다른 언어(java, C 등)랑은 다르게 **타입 강제**가 필요하지 않다. 변수에 값이 처음에 할당된 값과 동일한 타입일 필요도 없다. **변수에는 문자열을 넣었다가 나중에 숫자를 넣어도 상관없다**는 말이다.

~~~javascript
var a = 92;
typeof a; // 'number'

a = "92";
typeof a; // 'string'

a = true;
typeof a; // 'boolean'
~~~

위 예제를 보면 변수 a에 92를 할당한 뒤에 typeof 연산자를 보면 'number'가 나온다. 하지만 이건 변수 a의 타입을 물어보는게 아니라 "이 변수에 할당된 값의 타입은 무엇인가?"라고 물어보는 거다.

~~~javascript
typeof typeof 92; //string
~~~

typeof 연산자의 반환 값은 'string'이다. 해석해보면 typeof 92; 는 'number'를 반환하고 그걸 typeof 연산로 다시 반환하면 **typeof 'number';**이기 때문에 **결과값이 'string'**이 나오는거다.



## 3.강제변환







#### 참고자료

- YOU DON'T KNOW JS(타입과 문법, 스코프와 클로저)