---
description: 모듈화의 기본 함수에 대해서 알아보겠습니다 .
---

# 05. 함수 \(Function\)

![](.gitbook/assets/body%20%282%29.png)

## 함수 \(Function\)

함수란 어떤 작업을 수행하기 위해 필요한 구문들을 **그룹화**해 놓은 것 입니다.

예를 들어보겠습니다. 치킨집 사장님 혼자서 주문을 받고 닭을 튀기고 배달을 하신다면 생각만해도 복잡합니다.

사모님이 주문을 받아주시고 사장님은 닭을 튀기시고 아들이 배달을 한다고 했을때 각자 자신의 일만 신경쓰면 되기 때문에 조금 더 효율적이게 일을 할 수 있지 않을까요?

함수는 아래와 같이 생겼습니다.

```javascript
function foo(){ // 첫번째 그룹이 할 일 }
function foo2(){ // 두번째 그룹이 할 일 }
foo() // 첫번째 함수 실행
foo2() // 두번째 함수 실행
```

위에서 들었던 간단한 예제를 코드로 표현해보겠습니다.

```javascript
// 위의 치킨집을 아래와같이 역할분배를 해줄 수 있습니다.   
function 주문받기(전화받은내용){ // 주문을 받아서 사장님께 전달}
function 닭튀기기(사모님께전해받은내용){ // 전해받은 내용을 수행한다 }
function 배달(치킨){ // 전해받은 치킨을 배달한다}

function 치킨집(){
  주문받기() // 주문받아서 주문내용을 저장 
  닭튀기기() // 내용을 토대로 닭튀기기
  배달() // 치킨배달
}
```

이처럼 자신이 맡은 일만 수행할 수 있도록 그룹화 시켜주는 것이 함수 \(Function\) 입니다.

#### Return 

함수를 이용하면 아래 코드와 같이 내부의 값을 밖으로 던져 줄 수 있습니다.

```javascript
function foo () {
  return 'hello'
}
var text = foo()
```

> 실습\) 치킨 가게를 만들어 보아요

```javascript
function order(){ 
  console.log('주문을 받습니다.')
  return '치킨'
}

function cooking(chicken){ 
  console.log(chicken +'을 받아 요리를 만듭니다.')
  return '완성된' + chicken
}

function delivery(food){ 
  console.log(food + '을 받아 배달을 합니다.')
  return food + '을 배달 완료!'
}

function chickenShop(){
  var ingredients = order()
  var food = cooking(ingredients)
  var status = delivery(food)
  console.log('status', status) // 치킨을 배달 완료!
}

chickenShop() // run
```

### 함수를 쓰면 왜 좋을까요 ?

**첫번째**는 위에서 설명드린 **그룹화** 또는 **모듈화**가 가능해집니다. 관련된 함수끼리 묶어 놓을 수 있기 때문에 코드의 **유지보수성**, **가독성** 등이 올라갑니다.

**두번째**는 코드를 **재사용** 할 수 있습니다. 간단한 예를 들어보겠습니다.  
우리는 두 수를 더해주는 함수를 만들고 싶습니다.  
함수를 이용하지 않고 코드를 작성해보겠습니다.

```javascript
console.log(5 + 5)
console.log(10 + 10)
// console.log(10 + 10) x 100
```

두 수를 더해주는 코드의 경우 위와 같이 쉽게 작성할 수 있습니다. 정말 간단한 코드라 위처럼 작성해도 무리는 없으나, 두 수를 더하는 코드가 많아지고 기존 코드에 새로운 조건이 늘어난다면 + 되있는 곳을 모두 찾아 수정해줘야되는 번거로움이 있습니다.

그렇기 때문에 우리는 공통되는 역할을 하는 친구들을 함수로 만들어 둘 필요가 있습니다.

> 잠깐 매개변수라는 것을 알아보겠습니다.  
> 아래 코드의 foo \(a, b\) 라는 곳에서 a와 b가 매개변수라고 부르는 친구들입니다.  
> foo \(a, b\) 이때의 a와 b는 아무런 의미가 없습니다. 단순히 foo 라는 함수안에서 a와 b라는 이름으로 사용하기 위한 이름일 뿐입니다.  
>   
> foo \(10, 20\) =&gt; a = 10, b =20 처럼 함수를 실행하며 값을 넣어줄때 a와 b는 의미를 가지게됩니다.
>
> ```javascript
> function foo (a, b) {
>     console.log(a, b)
> }
> ```

매개변수에 대해서 알아봤으니 다시 내용으로 돌아가보겠습니다.

```javascript
function add(a, b) {
    console.log(num1 + num2)
}
add(10, 10)
add(20, 20)
```

add라는 함수는 두가지의 매개변수를 받아 두 매개변수를 합쳐주는 역할을 합니다.  
위처럼 함수를 만들어서 사용하게 된다면 수정사항이 생겨도 add 함수 하나만 수정을 하면되기 때문에 관리에 용이합니다.

또, 재사용에도 좋습니다. 지금은 두 수를 더해주는 함수로 이용했지만 String 을 합쳐주는 함수로도 이용할 수 있습니다.

```javascript
add('Simple', 'JS') // SimpleJS
```

> 실습\) 값을 받아서 type 을 체크해주는 함수를 만들어주세요

> 실습\) 아래의 처럼 동작 할 수 있도록 sell 함수를 만들어주세요

```javascript
var money = 1000;

sell(200) // 남은 돈 800
sell(300) // 남은 돈 500
sell(100) // 남은 돈 400
sell(500) // 돈이 부족해요
```

### 일급 객체

자료형을 공부하면서 기본 자료형을 제외한 모든 것들은 객체 \(Object\) 라고 했습니다.  
그러므로 함수도 객체입니다. 함수는 **일급 객체** 라고도 부르는데 몇가지 특징을 가진 객체를 **일급객체** 라고 부릅니다.

#### 함수를 매개변수로 전달 할 수 있습니다.

```javascript
// func 같은 것을 매개변수라고 부릅니다.
// foo 는 함수를 전달 받는 함수입니다. 전달 받은 함수를 실행시킵니다.  
function foo(func) { func() };

foo(function(){
    console.log('함수안에 함수를 매개변수로 전달할 수 있습니다.')
})
```

#### 변수나 데이터 구조안에 담을 수 있습니다.

```javascript
var foo = function(){
    console.log('변수안에 함수를 담을 수 있습니다.')
}
// 아직 배우지 않았지만 객체 안에도 함수를 담을 수 있습니다.
var obj = {
    foo: function() {
        console.log('객체안에 담긴 함수입니다. 메서드라고도 부릅니다.')
    }
}
```

#### 반환값 \(return value\) 으로 사용할 수 있다.

return 이라는 것으로 값을 밖으로 던져줄 수 있습니다.

```javascript
function foo () {
    return 10
}
var num = foo() 
// foo 가 return을 통해 밖으로 10을 던져줬고  
// num 이라는 변수가 foo가 던진 10을 받았습니다.
console.log(num) // 10 그러므로 num 에는 10이 들어있습니다.
```

위의 코드가 기본적인 return의 동작입니다. return 을 통해 함수자체를 받을 수도 있습니다.

```javascript
function foo () {
    return function () {
        console.log('return 된 함수')
    }
}
var func = foo() // foo 를 실행하면 return 된 함수가 func 에 들어가게 됩니다.
func() // return 받은 함수를 실행시킵니다.
```

위와 같은 특징들을 가진 객체를 일급 객체라고 표현합니다 :\)

> 실습\) calc\(1, 2, add\) 숫자와, 함수를 받는 함수를 정의해주세요

### 함수를 사용하는 방법

함수를 사용하는 방법에는 크게 세가지가 있습니다.

* 함수선언식\(Function declaration\)
* 함수표현식\(Function expression\)
* Function\(\) 생성자 함수 \( 잘 사용하지 않기 때문에 다루지 않겠습니다 \)

#### 함수 선언식

함수 선언식의 경우 함수는 이름을 가지고 있어야합니다.  
이름을 가지고 있는 이유는 재귀적 호출을 하거나, 디버거가 함수를 구분할 수 있도록 식별자 역할을 해주기 때문입니다. \( 우리가 이름을 가지고 있는 것 처럼요 \)

```javascript
function foo () { // foo 는 함수의 이름 입니다.
    foo() // 자기 자신을 호출할 수 있습니다. 이를 재귀라고 표현합니다.
}
```

#### 함수표현식

함수 표현식은 다른 방법으로 함수를 표현한다고 생각해주세요

```javascript
var foo = function () {
    console.log('foo 라는 변수를 통해서 함수를 표현했어요')
}
foo()
```

위처럼 변수에 함수를 넣어서 함수를 표현할 수 있습니다. 이때 변수에 할당되는 함수들은 보통 **이름을 생략합니다.** 이처럼 이름이 없는 함수를 **익명함수\(anonymous function\)** 라고 부릅니다.  
foo 라는 변수는 할당된 함수를 가리키는 **참조 값**을 저장하게됩니다. foo\(\) 를 호출시 참조 값을 가지고 실제 함수를 실행시킵니다.

> 간단한 예제
>
> +, -, \*, / 을 해주는 함수를 만들어 보세요  
> 자신의 성과 이름을 받아 출력해주는 함수를 만들어보세요

#### Arguments 

a 와 b 를 더해주는 함수가 있습니다. 

```javascript
function add(a, b) {
  return a + b
}
```

요구사항이 변경되어 3가지 수를 합하는 함수가 필요할때는 어떻게 해야될까요 ?

```javascript
function add(a, b, c) {
  return a + b + c
}
```

요렇게 만들어야 할까요 ..? 물론 가능하지만 나중을 생각한다면 좋은 방법은 아닌것 같습니다.

이 때 이용할 수 있는 것이 arguments 입니다. arguments 란 우리가 함수에 넘긴 인자에 대한 정보를 가지고 있습니다.

```javascript
function foo() {
	console.log(arguments)
}

foo(1,2,3,4,5) // Arguments(5) [1, 2, 3, 4, 5, callee: ƒ, Symbol(Symbol.iterator): ƒ]
```

foo 에 매개변수를 지정해주지 않았지만 `Arguments` 는 매개변수에 대한 정보를 알고 있습니다. 아직 배우지 않았지만 이 친구는 like array 라 부르는 유사 배열입니다. 기본 array 와는 성질이 다릅니다.

```javascript
function foo() {
	var result = 0
	for(var i = 0; i < arguments.length; i += 1){ 
		result += arguments[i]
	}
    console.log('총 합:', result)
}

foo(1,2,3,4,5) // 15 
```

Arguments 를 이용하면 매개변수에 묶이지 않고 유연하게 대처 할 수 있습니다.

**Rest parameter**

ES6 에는 Arguments 보다 조금 더 스마트한 Rest parameter 라는 녀석이 있습니다.

```javascript
function foo(a, ...rest) {
	console.log(a) // 1
	console.log(rest) // [2, 3, 4, 5] a 를 제외한 나머지 
}

foo(1,2,3,4,5) // 15 
```

> 실습\) Rest parameter 와 Arguments 를 이용하여 아래의 함수를 만들어주세요

```javascript
function add(){}
function sub(){}
function mul(){}
function mod(){}

calc(add, 1, 2, 3, 4, 5) => 1 ~ 5 를 더한 값
calc(sub, 1, 2, 3, 4, 5) => 1 ~ 5 를 뺀 값
```



