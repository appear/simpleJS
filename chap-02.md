---
description: 자바스크립트에서의 연산자 이용법에 대해서 살펴보겠습니다.
---

# 02. 연산자

![](.gitbook/assets/body%20%282%29.png)

## 연산자

자바스크립트 연산자에는 종류가 있는데요 자주 쓰이는 것들을 우선적으로 보겠습니다. 처음 배우시는 분들은 한번씩 타이핑 해보시길 추천드려요.

> console.log\(\)안에 내용은 개발자 도구에서 확인해볼 수 있도록 도와주는 디버깅용 함수입니다

### **사칙연산 + - \* / %**

```javascript
console.log(5 + 2);
console.log(45 - 4);
console.log(5 * 3);
console.log(12 / 3);
console.log(12 % 3);
```

또는 **변수**를 이용해도 됩니다. **=** 은 **대입 연산자** 입니다.

```javascript
var num = 5;
var num2 = 15;
console.log(num + num2);
console.log(num - num2);
console.log(num * num2);
console.log(num / num2);
console.log(num % num2);
```

### +=, -=, \*=, /= 을 이용한 연산

유용하게 사용할 수 있으니 꼭 기억해주세요 :\)

```javascript
var num = 0; // num에 기존값에 새로운 값을 연산해주고싶을때  
num = num + 5; // 방법 1
num += 5; // 방법 2 '+=' 이런식으로 줄여줄 수 있어요
```

더하기 연산자는 문자열을 합칠수도 있어요 \( 하지만 String 의 + 연산은 비싼 값을 요구한다니 좋은 방법은 아닌거 같아요 \)

```javascript
console.log('안녕' + '하세요');

// 요즘은 `` 을 이용하여 위와 같은 코드를 대체 할 수 있습니다.
var firstname = 'o'
var lastname = 'laf'
console.log(`${firstname}${lastname}`) // olaf

// firstname.concat(lastname)
```

### **비교연산자**

비교연산자는 **== \(Equal Operator\) 느슨한 비교** 연산자와 **=== 엄격한\(Strict Equal Operator\) 비교** 연산자가 존재합니다.  
자바스크립트에서는 될 수 있으면 === 을 써야합니다. 이유를 알려드릴게요

```javascript
var str = '5';
var num = 5;
console.log(str == num); 

// 결과값이 어떻게 나올까요 ? 
// false 인줄 알았는데요 이상하게도 결과값은 true 로 떨어집니다.
```

위에 경우 ‘5’와 5가 들어왔을때 자바스크립트는 영리하게도 …?  
같은 5 라는 데이터로 인식을 한다고합니다. 그렇기 때문에 예상치도 못한 결과를 가져올 수 가 있어요.  
**===** 의 경우 값의 타입 / 형식을 체크해줘서 비교하기 때문에 정확한 결과를 가져올 수 있습니다.

```javascript
console.log(str === num); //false
```

= 대입, == 느슨한 체크, === 엄격한체크 꼭 기억해 주세요 :\)

### 크**기 비교 연산자**

&lt;, &gt; \(크다작다\), &lt;= , &gt;= \( 작거나 같고, 크거나 같다\) 는 알고 계실 것이라 생각하고 넘어가겠습니다.

### **AND OR 연산자**

&&은 모두가 참일때 성립, \|\|은 하나라도 참이면 성립됩니다.

```javascript
var bool = true;
var bool2 = false;

// 실행됨 console.log()의 값이 찍힘
if(bool){ console.log('if문은 아직 신경쓰지마세요 true 라는 값을 봐주세요 !') }
// 실행안됨 
if(bool2){ console.log('if문은 아직 신경쓰지마세요 false 라는 값을 봐주세요 !') } 

// 이렇게 연속해서도 사용할 수 있어요 이때 &&와 || 가 등장합니다. 
// && 연산이기때문에 모두가 참이어야하는데 bool2가 거짓이니 실행되지않습니다. 
if(bool && bool2){ console.log('if문은 아직 신경쓰지마세요 bool 값을 봐주세요 !') } 

// 이렇게 연속해서도 사용할 수 있어요 이때 &&와 || 가 등장합니다. 
// || 연산이기때문에 하나라도 참이라면 실행이됩니다.  
if(bool || bool2){ console.log('if문은 아직 신경쓰지마세요 bool 값을 봐주세요 !') }
```

### **증감연산자**

-- 와 ++ 는 증감 연산자라고 부릅니다 \(증가, 감소\) 위치에 따라서 동작하는 방식이 약간 달라집니다. \( ++, -- 보다는 +=, -= 을 이용하는게 더 좋다고 합니다. 어떤 책에서는 ++, -- 를 겉멋이라는 용어를 사용하기도 합니다\)

```javascript
var num = 10;
// 복잡한 로직(과정)이 있다고 가정하겠습니다.
// 상황 1 : —num (연산전 num을 1감소 시키고 시작하겠다는 의미입나다) => 로직실행(이때의 num은 9이겠죠?);
// 상황 2 : num— (연산후에 num을 1감소 시키겠다는 의미입나다) => 로직실행(이때의 num은 10이겠죠) => 이후에 num 1감소
// ++num , num++ 도 마찬가지입니다.
```

### **!과 !!**

**!**는 ture, false를 반대로 **!!**는 값들 \(배열, 객체또는 String, Number 등등..\) 을 **boolean** 값으로 변경해줘요

```javascript
var check = true;
console.log(!check); // !는 boolean 값을 뒤집어줍니다. false
var string = 'olaf';
console.log(!!string); // true 
// 아래에서도 설명드리겠지만 빈 문자열 "" 은 false로 판별됩니다.
var empty = '';
console.log(!!empty); // false
```

### Truthy 와 Falsy values

기본적인 true, false 말고 조건문에서 false로 판단되는 값들이 몇가지 더 있습니다.  
중요한 개념이니 꼭 숙지해주세요 !

* undefined
* null
* 0
* NaN \(Not a Number\)
* “” \(빈문자열\)

