# 13. This

## This

This 는 함수 호출 패턴에 따라서 달라집니다. 호출패턴에는 4종류가 있습니다.

* 함수 호출 패턴
* 메소드 호출 패턴
* 생성자 호출 패턴
* apply, call, bind 패턴 \(이번 챕터에서는 다루지 않습니다\)

### 함수 호출 패턴

함수 호출패턴에서는 기본적으로 전역함수 내부함수 모두 this는 window\(전역객체\)를 가리킵니다.

```javascript
var outter = function(){
    console.log('outter', this)
    var inner = function(){
        console.log('inner', this);
    };
    inner();
};
outter();
```

Strict 모드 일때는 보통의 함수 호출패턴의 this와는 다릅니다.

```javascript
'use strict' // Strict 모드를 사용하겠다고 선언했습니다.
function func(){
  console.log(this); // undefined
}
func();
```

### 메소드 호출 패턴

호출된 함수가 객체의 프로퍼티이면 메소드 호출 패턴으로 호출됩니다.  
메소드 내부의 this는 해당 메소드를 소유한 객체 즉 해당 메소드를 호출한 객체에 바인딩됩니다.

```javascript
var person = {
  name : 'olaf',
  getName : function(){
    console.log(this); // person
    console.log(this.name); // olaf
  }
};
person.getName();
```

메서드안에 또다른 inner 함수가 존재한다면 그때의 this는 무엇일까요?

```javascript
var person = {
  name : 'olaf',
  getName : function(){
    console.log(this);
    console.log(this.name); 
    function inner(){
        console.log(this); // window
    }
    inner(); // 메서드 내부함수 실행
  }
};
person.getName();
```

함수 호출패턴과 마찬가지로 this는 전역객체인 window를 가리킵니다.

### 생성자 호출 패턴

```javascript
var Person = function(name){
    this.name = name;  // this는 자신 즉, Person을 가리킨다.
  };

Person.prototype.getName = function(){
  console.log(this.name); // Person.prototype 이기때문에 프로토타입 내에서도 this는 자기자신 Person을 가리킵니다.
};
```

프로토타입 안에서의 inner 함수 호출의 this도 일반 함수 호출 패턴을 따릅니다.

```javascript
var Person = function(name){
    this.name = name;  // this는 자신 즉, Person을 가리킨다.
  };

Person.prototype.getName = function(){
  console.log(this.name); // Person.prototype 이기때문에 프로토타입 내에서도 this는 자기자신 Person을 가리킵니다.
  function inner(){
    console.log(this); // window가 찍힙니다! 이제 눈에 보이시죠?!
  }
  inner();
};

var p = new Person('olaf');
p.getName();
```

