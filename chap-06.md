---
description: 자바스크립트의 Object 에 대해서 알아보겠습니다.
---

# 06. 객체 \(Object\)

![](.gitbook/assets/body%20%282%29.png)

## Object

자바스크립트에서 기본 데이터타입 \(boolean, number, string, null, undefined\)을 제외한 모든것은 객체입니다.

객체는 이름 \(key\)과 값\(value\)의 쌍인 속성들을 포함하는 컨테이너라고도 할 수 있습니다.  
또 데이터를 한 곳에 **모으고 구조화 \(중요합니다!!\)** 하는데 유용합니다.  
기본 데이터 타입중에 null, undefined을 제외한 boolean, number, string 도 객체처럼 다룰 수 있습니다.

객체는 아래와 같이 생겼습니다.

```javascript
var obj = {
    key: value
}
console.log(obj.key) // value => key값을 통해 value를 불러올 수 있습니다.
```

### 속성 \(Property\) 과 메서드

**속성**은 key\(속성명\), value\(속성값\) 로 표현할 수 있습니다.

```javascript
// shop 에는 name 이라는 Property 가 있습니다.
var shop = {
    name: '과일 가게'
}
console.log(shop.name) // 과일 가게
```

메서**드**는 객체의 속성값으로 포함된 **함수**를 의미합니다.

```javascript
var shop = {
    sell: function () {
        console.log('사과 사세요~~')
    }
}
shop.sell() // 사과 사세요
```

### 객체 생성법

객체를 생성하는 방법으로는 크게 세가지가 있습니다.

* new Object\(\)를 이용한 생성자방법 
* {}로 생성하는 리터럴 방식 
* 생성자 함수

하나씩 비교해가면서 알아보겠습니다.

#### new Object

```javascript
var obj = new Object(); // new Object 를 통해 Object 를 선언합니다.
// true => 생성된 Object 타입을 체크합니다.
console.log(obj.constructor === Object); 

// obj.key = value 의 형식으로 값을 추가할 수 있습니다.
obj.name = 'olaf';  
obj.age = 27;
```

> constructor는 해당 Object가 어떤 Object를 상속 받았는지를 판단할 수 있게 알려주는 속성입니다.

new Object\( 매개변수 \) 를 넣어서 객체를 생성할 수 있습니다.

```javascript
var number = new Object(1);
console.log(number.constructor === Number); // true
console.log(number.constructor === Object); // false 

var string = new Object("I am a string");
console.log(string.constructor === String); // true
console.log(string.constructor === Object); // false

var boolean = new Object(true);
console.log(boolean.constructor === Boolean); // true
console.log(boolean.constructor === Object);  // false
```

혹시 눈치채셨나요 ? 위의 코드가 **new Objec**t 의 문제점입니다.  
기본 자료형 number, string, boolean 도 Object 로 이용할 수 있다고 말씀드렸습니다.

new Object\( number, string, boolean \) 을 인자로 넣어 만들어진 객체는 다른 내장 생성자에게 객체 생성을 위임하여 우리가 기대했던 결과와 다른 객체를 생성해버립니다.

new Object 를 이용한 객체 생성법의 문제점을 정리해보면 아래와 같습니다.

* number, string, bool등 new Object로 생성시 우리가 의도했던 결과와는 다른 결과가 나옵니다.
* 값을 하나하나 추가해줘야하니 가독성이 떨어집니다.

#### 리터럴 방식 <a id="&#xB9AC;&#xD130;&#xB7F4;-&#xBC29;&#xC2DD;"></a>

가장 많이 이용하는 객체 생성법입니다.

```javascript
var obj = {}; // 리터럴 방식으로 빈객체 생성
console.log(typeof obj); // object
// 이렇게 속성들을 추가 할 수 있어요, 그럼 new Object랑 같은거 아니에요 ? 
obj.name = 'olaf';
obj.age = 27;

// 리터럴 방식을 이용하면 아래와 같은 표현도 가능합니다.
// 이렇게 한번에 넣어줄 수 있어요. 속성들이 한눈에 보이죠 ?
var person = { 
  name : 'olaf',
  age : 27,
  getName : function(){ // 메서드도 표현할 수 있어요
    // this 는 아직 모르셔도되요 자기 자신이라고만 알아주세요
    console.log(this.name); // olaf
  }
};
console.log(typeof person); // object
console.log(person); // { name: 'olaf', age: 27}
// 속성 사용법
console.log(person.name); // olaf key 값으로 접근할 수 있습니다.
console.log(person.age); // 27
console.log(person.getName()); // 메서드 실행
```

리터럴 생성 방식을 정리해보면

* 한번에 값들을 넣어줄 수 있기 때문에 가독성이 좋다. 
* new Object 같이 엉뚱한 값을 리턴할 일이없다.

#### 사용자 정의함수 \(생성자함수\) <a id="&#xC0AC;&#xC6A9;&#xC790;-&#xC815;&#xC758;&#xD568;&#xC218;-&#xC0DD;&#xC131;&#xC790;&#xD568;&#xC218;"></a>

모듈화에 많이 쓰이는 방식입니다. 여러 모듈화 방법에 대해서는 뒤에서 알아보겠습니다 :\)

new 키워드로 객체를 생성하는 방법을 생성자 방식이라고 합니다.  
생성자 함수를 만드는데는 몇가지 알아야할 사항이있습니다.

첫번째로 생성자 함수 이름은 일반적으로 대문자로 시작합니다. 이것은 생성자 함수임을 인식하도록 도움을 줍니다.

두번째 속성 또는 메서드명 앞에 기술한 this는 생성자 함수로 생성될 인스턴스\(자기자신\)를 가리킨다.

```javascript
// name 매개변수를 받는 Person 생성자 함수입니다.
var Person = function(name) { 
  // 생성시 최초로 실행될 영역이에요 
  // this가 자기자신이라고했죠? this 는 Person 입니다. 
  // Person.name을 넘겨받은 name 으로 하겠다는 의미입니다.
  this.name = name; 
  this.say = function() { // 함수도 추가할 수 있어요
    // this.name은 생성시 넘겨받은 이름입니다. 
    console.log("I am" + this.name); 
  };
}
// 생성자함수를 이용해 객체를 만들어 보겠습니다.
var p = new Person('olaf'); // name을 받기로했으니 olaf 라는 값을 넣어줬어요
// Person {name: "olaf", say: ƒ} 
// 우리가 넣어준 olaf 가 person의 name 으로 들어갔습니다.
console.log(p);
p.say(); // I am olaf 가 찍히겠죠 ?
```

좀 더 자세한 사용법은 뒤의 JS의 모듈화를 알아보는 챕터에서 다뤄보겠습니다.

#### TIP\) 생성자 함수를 강제화 하는 방법

생성자함수를 사용하려면 new를 써줘야된다고 배웟습니다.  
만약에 실수를 해서 생성자 함수를 실행할때 new가 빠진다면 우리가 원하는대로 생성자함수가 안만들어지겠죠?

new를 강제로 하는 패턴을 알려드리겠습니다. \( 지금 이해 못 하셔도 괜찮습니다 \)

```javascript
var Person = function(name){
  // instanceof는 우변 피연산자의 프로토타입이 좌변 피연산자의 프로토타입 체인에 있는지 찾아주는 연산자입니다. 
  // 쉽게말하면 this가 Person을 통해서 만들어진건지 판단해줍니다.
  // 그게 아니라면 new를 통해서 만들어서 return 해줍니다.
    if(!(this instanceof Person)){ 
      // this 가 Person 을 통해서 만들어진 것이 아니라면
      return new Person(name);
    }
    // 만들어진것이 맞다면 원래대로 실행한다.
    this.name = name;
}
```

### 객체 속성을 다루는 방법 \(추가, 삭제, 탐색, 갱신\) <a id="&#xAC1D;&#xCCB4;-&#xC18D;&#xC131;-&#xCD94;&#xAC00;-&#xC0AD;&#xC81C;-&#xD0D0;&#xC0C9;-&#xAC31;&#xC2E0;"></a>

#### 추가 <a id="&#xCD94;&#xAC00;"></a>

```javascript
var obj = {}; // 빈객체
obj.name = "olaf";
console.log(obj); // Object {name: "olaf"}

// 해체 할당자
var obj2 = { ...obj, age: 27 } // ...obj 란 obj 를 기존의 주소와 다른 새로운 객체를 만듭니다
console.log(obj2) // name: olaf, age: 27
```

#### 삭제 <a id="&#xC0AD;&#xC81C;"></a>

```javascript
var obj = {}; // 빈객체
obj.name = "olaf";
console.log(obj); // Object {name: "olaf"}
delete obj.name; // delete 를 사용해서 삭제
console.log(obj); // Object {}
```

#### 갱신 <a id="&#xAC31;&#xC2E0;"></a>

이미 존재하는 속성명 \(key\) 이라면 값을 갱신합니다. 값이 없다면 새로 속성명과 값을 추가합니다.

```javascript
var obj = {}; // 빈객체
obj.name = "olaf";
console.log(obj); // Object {name: "olaf"}
// 갱신
obj.name = "modify olaf"; // 속성값 변경
console.log(obj); // Object {name: "modify olaf"}
```

#### 탐색 <a id="&#xD0D0;&#xC0C9;"></a>

객체명\[속성명\]으로 접근하면 속성명에 해당하는 속성값을 뺴올 수 있어요. 이때 주의 하실점이있습니다.

```javascript
var obj = {
  "name-first" : 'olaf' // 처럼 속성명에 - 이 들어간경우
};
// 로 가져오게되면 -을 연산처리해버리기 때문에 원하는 결과를 얻을 수 없어요 
console.log(obj.name-first); 
// 이런식으로 해주시면됩니다.
console.log(obj['name-first']);


// 해체 할당자
var obj = { a: 10 } 
var { a } = obj
console.log(a) // 10

```

#### for in 을 이용한 탐색

```javascript
var person = {
  name : 'olaf',
  age : 27
};
var key;
for (key in person) {
  console.log(key + ': ' + person[key]); // key에 속성명이 들어갑니다. 
}
/*
  name : olaf,
  age : 27
*/
```

#### Object Keys 를 이용한 탐색 

```javascript
var obj = { a: 10, b: 20, c: 30 }

Object.keys(obj) // ["a", "b", "c"]

Object.keys(obj).forEach(function(key) {
  console.log(obj[key]) 
}) // 10, 20, 30
```

#### Object Values 

```javascript
var obj = { a: 10, b: 20, c: 30 }

Object.values(obj) // [10, 20, 30]

Object.values(obj).forEach(function(value) {
  console.log(value) 
})
```

#### Object entries

```javascript
var obj = { a: 10, b: 20, c: 30 }

Object.entries(obj) //  ["a", 10], ["b", 20], ["c", 30]

Object.entries(obj).forEach(function([key, value]) {
	console.log(`${key}: ${value}`)
}) // a: 10, b: 20, c: 30
```

### 어떻게 사용하는거에요 ?

객체를 만드는 방법들과 값의 추가 삭제등 객체를 다루는 방법에 대해 알아봤습니다.  
저는 처음에 공부할때 이 배운것들을 도대체 어디에 어떻게 사용을 해야되는지 잘 모르겠더라고요. 저와 같은 고민을 가지고 있으실 분들을 위해 간단하게 자주 이용되는 경우를 알아볼게요

{ } 를 통한 리터럴 방식의 객체 선언은 보통 데이터를 정의할 때 많이 이용합니다.

```javascript
// 박스를 만들기 위한 데이터 정의
var option = {
    width: 200,
    height: 150
    color: 'red'
}
```

사용자 정의 함수의 경우 모듈화에 많이 이용합니다.  
리터럴 방식과 사용자정의 함수를 이용해서 간단한 모듈을 만들어 사용해보겠습니다.

> **간단한 예제**  
> 옵션 값에 따라 박스를 만들 수 있는 사용자 정의 함수를 구현하세요

```javascript
// 옵션 값 정의
var option = {
    width: 200,
    height: 150
    color: 'red'
}
// 옵션 값을 받는 사용자 정의 함수
// 옵션 값에 따라 박스가 다르게 만들어진다.
var boxMaker = function(option) {
    this.width = option.width;
    this.height = option.height;
    this.color = option.color;
    this.getColor = function(){
        return this.color;
    }
}
boxMaker(option); // 박스 만들기


// class 

class BoxMaker {
  constructor(option) {
    this.width = option.width;
    this.height = option.height;
    this.color = option.color;

    this.getColor = function(){
        return this.color;
    }
  }
}

console.log(new BoxMaker({ 
  width: 300,
  height: 200,
  color: '#fff'
}).getColor())
```

위처럼 같은 객체지만 만드는 방식에 따라 역할이 조금씩 달라집니다 :\)

> **간단한 예제**
>
> 객체 생성방식은 { } 와 생성자 함수를 둘다 이용해서 만들어보시면 좋습니다.
>
> 1. 빈 사람 객체를 하나 만든다.
> 2. 객체에 name,age 속성을 추가한다.
> 3. 객체에 getName이라는 메서드를 만든다. getName은 자기 자신의 이름을 console에 찍어준다.
> 4. name 속성의 값을 변경한다.
> 5. 다시 getName을 이용해서 name 속성의 값을 찍어본다.
> 6. name속성을 삭제한다.
> 7. 조건문을 사용해서 name속성이 없다면 다시 name 속성을 추가해준다.
> 8. 최종 Object를 탐색하여 console에 찍는다.

정답 : [https://jsfiddle.net/xbmjL2vc/](https://jsfiddle.net/xbmjL2vc/)



