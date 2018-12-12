---
description: 자바스크립트를 다루기위한 가장 기초적인 문법을 공부해보겠습니다.
---

# 01. 자료형과 변수

![body](.gitbook/assets/body%20%282%29.png)

## 자료형과 변수

### 기본자료형

기본 자료형이란 Object 를 제외한 변경 불가능한 값 \( immutable value \) 을 말합니다.

> 기본 자료형에 대한 [**미디엄 글**](https://medium.com/@appear.ko/javascript-primitives-type-에-대한-이야기-225de7eb471c)도 한번 읽어보시면 좋습니다. \( 제가 정리한 글 입니다 ... \)

* **Boolean** : true 와 false 의 두 가지 값을 가질 수 있다.
* **Null** : Null 타입은 딱 한 가지 값, null 을 가질 수 있다.
* **Undefined** : 값을 `할당`하지 않은 변수는 undefined 값을 가진다.
* **Number**
* **String**
* **Symbol** \(ECMAScript 6에 추가\) : Symbol은 유일하고 변경 불가능한 \(immutable\) 기본값 \(primitive value\) 이다

typeof를 이용하면 값의 타입을 알 수 있습니다. 아직은 new라든지 valueOf같은 함수는 모르셔도됩니다. 결과값만 봐주세요

```javascript
typeof true; //"boolean"
typeof Boolean(true); //"boolean"
typeof new Boolean(true); //"object"
typeof (new Boolean(true)).valueOf(); //"boolean"

typeof "appear"; //"string"
typeof String("appear"); //"string"
typeof new String("appear"); //"object"
typeof (new String("appear")).valueOf(); //"string"

typeof 123; //"number"
typeof Number(123); //"number"
typeof new Number(123); //"object"
typeof (new Number(123)).valueOf(); //"number"
```

### Object \( 객체형, 참조형 \)

기본본자료형 \(Primitives\) 을 **제외**한 나머지 값들 \( 배열, 함수, 정규표현식 등 \) 은 모두 객체입니다.

Object는 뒤에서 조금 더 자세하게 다룰 예정입니다.

### 자바스크립트의 타입

보통의 언어들과는 다르게 자바스크립트는 변수의 타입을 미리 선언할 필요가 없습니다.  
타입은 프로그램이 처리되는 과정에서 자동으로 정해질거에요.  
이를 느슨한 **데이터 타입** \(loosley data type\) 또는 동적 타입 언어라고 합니다.  
선언을 해줄때는 편하지만 타입이 선언되지않다보니 사용시에 타입체크를 해줘야하는 불편함이 있을 수 있습니다. 이를 보완한것이 [타입스크립트](https://hyunseob.github.io/2016/09/25/typescript-introduction/) 입니다.

```javascript
var foo = 25;    // foo 는 이제 Number 
var foo = "apepar"; // foo 는 이제 String 
var foo = true;  // foo 는 이제 Boolean 

// ex) Java는 변수 선언시 타입을 정해줘야합니다.
public string name = "appear";
private int age = 25;
```

### 변수

프로그래밍을 접하면 가장 먼저 만나는 단어가 변수라는 단어일텐데요 변수가 무엇을 뜻할까요?

> **변수란**  
> 나중에 쓰기위해 값을 담아놓는 공간, 메모리상의 주소를 의미합니다.  
> 조금더 사용하기 쉽게 var name = appear 같은 name \(식별자\) 를 사용합니다.

* 변수에 값을 대입하는것을 초기화라고 부릅니다.
* 낙타 표기법이라 불리는 **camelCase** 를 사용합니다.  ex\) firstName 같이 첫번째 단어는 소문자 다음 단어부터는 첫글자를 대문자로 사용합니다.

```javascript
var String = ''; // 문자열
var Number = 0; // 숫자
var Bool = false; // 불린
var Null = null; // 널
var Undefined = undefined; // 언디파인드
var Array = []; // 배열
var Obj = {}; // 객체
var Func = function() {}; // 함수
```

그렇다면 변수를 실제로 어떻게 사용할까요?

한가지 간단한 예를 들어보겠습니다.

1. 우리는 더하기 값을 계속 누적하고 싶어요 
2. 예를 들자면 10 + 10 = 20 후에 20에 또 5를 더할 수도있고 -3을 할 수도 있어요

```javascript
// 20 까지는 구했어요 하지만 20 이라는 값에 계속 연산을 하고 싶지만 방법이 없어요
10 + 10 
// num 이라는 변수를 선언하여 연산 결과를 저장해 뒀어요 
var num = 10 + 10 
// num 에는 이미 20이 들어 있기 때문에 20 + 5 라는 연산을 할 수 있었어요
var num2 = num + 5
```

