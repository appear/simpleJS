# 모아보는 ES6



### 1. block scope

기존의 함수에 의한 스코프처럼 `{ }`으로 감싼 내부에 별도의 스코프가 생성된다.

```javascript
{
  let a = 10;
  {
    let a = 20;
    console.log(a); // (1)
  }
  console.log(a); // (2)
}
console.log(a); // (3)
```

```javascript
let sum = 0;
for (let j = 1; j <= 10; j++) {
  sum += j;
}
console.log(sum); // (1)
console.log(j); // (2)
```

```javascript
if (Math.random() < 0.5) {
  let j = 0;
  console.log(j); // (1)
} else {
  let j = 1;
  console.log(j); // (2)
}
console.log(j); // (3)
```

### 2. block scoped variables

`let`은 기존의 `var`를 대체하는 블락변수이고, `const`는 그 중 한 번 선언 및 정의되고 나면 값을 변경할 수 없는 변수이다. 블락 스코프 내부에서 선언된 `let`, `const`는 해당 스코프 내에서만 존재하며, 이들에 대해서는 'TDZ'가 존재한다.

> `TDZ (temporal dead zone, 임시사각지대)` : 블락 스코프 내에서는 지역변수/상수에 대한 호이스팅이 이뤄지기는 하나, 선언된 위치 이전까지는 해당 변수/상수를 인식하지 못한다.

```javascript
console.log(a); // (1)
let a = 2;
console.log(a); // (2)
```

```javascript
for (let j = 0; j < 5; j++) {
  console.log(j);
}
console.log(j); // (1)
```

```javascript
const PI = 3.141593;
PI = 3.14; // (1)
```

### 3. arrow function

순수 함수로서의 기능만을 담당하기 위해 간소화한 함수. `=>`의 좌측엔 매개변수, 우측엔 return될 내용을 기입한다. 우측이 여러줄로 이루어져있다면 `{ }`로 묶을 수 있으며, 이 경우엔 명시적으로 return을 기술하지 않으면 `undefined`가 반환된다.

```javascript
let getDate = () => new Date();
let sum = (a, b) => a + b;
let getSquare = a => {
  return a * a;
};
let calc = (method, a, b) => {
  switch (method) {
    case "sum":
      return a + b;
    case "sub":
      return a - b;
    case "mul":
      return a * b;
    case "div":
      return a / b;
  }
  return null;
};
console.log(getDate());
console.log(sum(4, 5));
console.log(getSquare(10));
console.log(calc("mul", 3, 4));
```

```javascript
const obj = {
  grades: [80, 90, 100],
  getTotal: function() {
    this.total = 0;
    this.grades.forEach(v => {
      this.total += v;
    });
  }
};
obj.getTotal();
console.log(obj.total); // (1)
```

### 4. rest parameter

* 함수 파라미터에 일정하지 않은 값들을 넘기고자 할 경우에 유용.
* arguments의 대체.
* 배열의 얕은복사 목적으로 활용 가능.

```javascript
function f(x, y, ...rest) {
  console.log(rest); // (1)
}
f(1, 2, true, null, undefined, 10);
```

```javascript
const sum = function(...arg) {
  let result = 0;
  for (let i = 0; i < arg.length; i++) {
    result += arg[i];
  }
  return result;
};
/* const sum = (...arg) => arg.reduce((p,c)=> p+c); */

console.log(sum(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)); // (1)
```

### 5. spread operator

문자열의 각 단어, 배열의 요소들이나 객체의 프로퍼티들을 해체하여 여러개의 값으로 반환해준다.

```javascript
const str = "hello olaf";
const arr = [20, 10, 30, 40, 50];
console.log(...arr); // (1)
console.log([...str]); // (2)
```

```javascript
const originalArray = [1, 2];
const copiedArray = [...originalArray];

originalArray.push(3);
console.log(originalArray); // (1)
console.log(copiedArray); // (2)
```

### 6. default parameter

파라미터에 값을 할당하지 않거나 빈 값인 상태로 함수를 호출할 경우, 해당 파라미터를 지정한 기본값으로 인식하도록 해줌. 각 파라미터는 내부에서 let과 동일하게 동작하며, 따라서 TDZ가 존재한다.

```javascript
function f(x = 1, y = 2, z = 3) {
  console.log(x, y, z); //(1)
}
f(4, undefined, 5);
```

```javascript
function multiply(x = y * 3, y) {
  console.log(x * y);
}
multiply(2, 3); // (1)
multiply(undefined, 2); // (2)
```

### 7. Enhanced Object Literal

#### 7-1. property Shorthand

프로퍼티의 키와 값에 할당한 변수명이 동일한 경우, 키를 생략할 수 있다.

```javascript
const x = 10,
  y = 20;
const obj = {
  x,
  y
};
console.log(obj); // (1)
```

```javascript
function setInformation(name, age, gender) {
  return {
    name,
    age,
    gender
  };
}
const person = setInformation("나연", 23, "female");
console.log(person); // (1)
```

#### 7-2. method Shorthand

메서드명 뒤의 `: function` 키워드를 생략할 수 있게 되었다.

```javascript
const obj = {
  name: "olaf",
  getName() {
    return this.name;
  },
  printName(name) {
    console.log(this.getName());
  }
};
console.log(obj.getName()); // (1)
obj.printName(); // (2)
```

#### 7-3. `Object.assign` \(ES6\)

[Object.assign\(\)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) 객체의 복사를 수행한다.

```javascript
const originalObj = {
  a: 1,
  b: [2, 3, 4],
  c: { d: 5, e: 6 }
};
const copiedObj = Object.assign({}, originalObj);
copiedObj.a = 11;
copiedObj.b[0] = 12;
copiedObj.c.d = 13;
console.log(originalObj, copiedObj); // (1)
```

```javascript
const originalObj = {
  a: [2, 3, 4],
  b: { d: 5, e: 6 }
};
const copiedObj = Object.assign({}, originalObj, { b: { f: 7, g: 8 } });
console.log(copiedObj); // (1)
```

### 8. Destructuring Assignment

배열 혹은 객체를 해체하여 각각 변수에 할당한다.

**1\) 배열**

```javascript
const [a, b, c] = [1, 2, 3];
console.log(a, b, c); // (1)
```

**2\) 객체**

```javascript
const person = {
  name: "나연",
  age: 23,
  gender: "female"
};

const { name: n, age: a, gender: g } = person;
console.log(n, a, g); // (1)

const { name, age, gender } = person; // (2)
console.log(name, age, gender);
```

### 9. template literals

여러줄 문자열, 보간\(표현식 삽입\) 등을 지원하는 새로운 형태의 문자열.

```javascript
console.log(`a
bb
ccc`); // (1)
```

```javascript
const a = 10;
const b = 20;
const str = `${a} + ${b} = ${a + b}`;
console.log(str); // (1)
```

### 10. class

Java의 그것과 비슷하지만 private 메서드가 없다.

```javascript
class Person {
  constructor(name, age, job) {
    this.name = name;
    this.age = age;
    this.job = job;
  }

  toString() {
    return `${this.name}, ${this.age}세, 직업: ${this.job}`;
  }
  getName() {
    return this.name;
  }
}

const olaf = new Person("olaf", 27, "front");
olaf.getName();
olaf.toString();
```

