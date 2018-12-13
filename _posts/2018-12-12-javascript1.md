---
layout: post
title:  "Javascript 문법"
author: SomeBodyHelpMe
---


# Javascript 특징

- Scripting Language
- 가볍고 손쉽게 작성이 가능한 프로그래밍 언어
- HTML 내에 코드를 삽입하여 사용
- 거의 모든 브라우저에서 실행 가능
- 이벤트 중심 프로그래밍
- Node.js 의 등장으로 서버 사이드 개발 가능
- 클래스는 지원하지 않지만 객체 지향 프로그래밍 가능
- 모든 객체는 프로토타입을 가짐
- 일급객체와 클로저의 특성으로 함수 지향 프로그래밍 가능
- Javascript의 표준이 ECMAScript이고 현재는 ECMAScript6(줄여서 ES6)가 표준



# Javascript 문법 - 1

## 자료형

* Javascript는 변수 타입 표시를 하지 않고, 값이 할당되는 과정에서 자동으로 자료형이 결정

  => 그래서 같은 변수에 여러 자료형의 값을 대입할 수 있다

* String, Number, Boolean, undefined, null, Object

* ES6에서 Symbol이 추가됨 : primitive type 이기 때문에 new로 생성 X

* 자료형 var, let, const로 표시 -> Scope의 차이

* Primitive Type : Number, String, Boolean, undefined, null + Symbol

* Reference Type : Array, Function (Object)



###Number

* 다른 언어들처럼 여러 타입(int, short, long, float) 등이 있지 않음

* 정수값과 실수값 구분하지 않음 

* 모든 숫자를 실수로 표현(64bit의 floating point type으로 저장)

* 비트연산도 가능. But 느림



###String

* 2byte의 값들이 연속적으로 나열된 것

* 0기반의 인덱싱 사용(다른 언어와 동일)

* 문자 하나를 표현하는 문자형은 제공하지 않음(길이가 1인 문자열)

* ' ' (작은 따옴표) , " " (큰 따옴표)

* 여러 문자열을 ‘+’ 를 이용해 연결할 수 있음

  (+가 addition 과 concatenation 으로 사용되기 때문에 주의하여 사용해야함)

* 문자열을 수정하는 모든 메소드는 새로운 문자열을 반환



###Boolean

* true, false 중 하나의 값을 가짐

* 비교의 결과로 생성

* false : 0, "", undefined, null, NaN(Not A Number) 



###Null, undefined

* null은 ‘객체가 아님’을 뜻하는 특수한 값

* undefined는 ‘값이 없음’을 나타내는 값 – 값 자체가 없음, 초기화 되어있지 않거나 존재하지 않는 값에 접근할 때

* 시스템 레벨에서는 undefined, 일반적인 프로그램 레벨에서는 null을 사용



###Object

* 속성(property) : 키(key) – 값(value)의 쌍으로 이루어짐

* 속성 끼리는 쉼표( , )로 구분

* 키는 문자열만 가능. 따옴표 있어도, 없어도 가능



###Array

* [] 로 감싼다. 값들이 순서대로 나열

* 배열의 원소에는 다른 데이터 타입들이 들어갈 수 있음



## 함수

### 일급 객체

* Javascript는 함수형 프로그래밍 언어(Functional Programming)

* C : Imperative Programming / Java : Object-Oriented Programming

* Javascript에서는 객체가 일급 객체(First Class Object)이다 => 함수도 객체! => 함수가 일급 객체!!

* 익명 함수(Anonymous Function) : 함수의 이름이 없는 함수

* 고차 함수(Higher-Order Function) : 함수를 인자로 받거나 반환할 수 있는 함수



###일급 객체의 조건

* 변수나 데이터 구조안에 담을 수 있다

* 다른 함수의 파라미터로 전달할 수 있다

* 반환값(return value)으로 사용할 수 있다

* 할당에 사용된 이름과 관계없이 고유한 구별이 가능하다

* 동적으로 프로퍼티 할당이 가능하다

```
console.log('*** 변수나 데이터 구조안에 담을 수 있다. ***');
var func1 = function() {
	console.log(1);
}
func1();		// 1

console.log('*** 파라미터로 전달할 수 있다. ***');
var func2_1 = function() {
	return 2;
}
var func2_2 = function(value) {
	console.log(value);
}
func2_2(func2_1());		// 2

console.log('*** 반환값(return value)으로 사용할 수 있다. ***');
var func3 = function() {
	return function() {
		console.log(3);
	}
}
func3()();		// 3

console.log('*** 할당에 사용된 이름과 관계없이 고유한 구별이 가능하다. ***');
var func4 = function func44() {
	console.log(4);

}
func4();		// 4

console.log('*** 동적으로 프로퍼티 할당이 가능하다. ***');
var func5 = function() {
	console.log(5);
}
func5.['property'] = '55';
console.log(func5.property);		// 55


```

###함수의 생성 방법

- 함수 선언문을 사용한 생성

  ```
  function func1(n) {
    console.log('func1 : ' + n);
  }
  ```

  * 코드 블럭 자체는 실행 가능 코드가 아님
  * 함수명이 반드시 정의되어야 함
  * 일반적인 함수 정의와 같음
  * 매개변수의 타입 표시하지 않음

- 함수 표현식을 사용한 생성

  ```
  var func2 = function(n) {
    console.log('func2 : ' + n);
  }
  
  var func4 = function func44() {
  	console.log(4);
  }
  func4();		// 4
  ```

  - 함수 리터럴(표현식)로 특정 변수에 할당되거나 즉시 실행 가능한 코드 블럭
    - 리터럴 : 데이터형에 보관하는 값 그 자체, 또는 값의 표현 방법
  - 일급 객체이므로 변수에 할당 가능
  - 함수 이름은 선택 사항. 함수 표현시에서 사용된 함수 이름이 외부에서 접근할 수 없음

- 생성자 함수를 사용한 생성

  - 함수가 일급 객체이기 때문에 객체 생성 방식과 비슷
  - new 키워드로 객체를 생성할 수 있는 함수
  - prototype 을 사용하여 한 번만 메소드를 생성할 수 있음

