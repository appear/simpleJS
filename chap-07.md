---
description: '여태까지 배운 내용들을 이용하여 과일가게와 장난감가게를 만들어봐요 :)'
---

# 실습\) 과일가게와 장난감가게

![body](.gitbook/assets/body%20%282%29.png)

## 과일가게와 장난감가게

### 문제

한 마을에는 **과일 가게**와 **장난감 가게**가 있습니다.  
**과일 가게**에는 사과와 파인애플을 팔며 **사과**는 **200원**, **파인애플**은 **500원**에 판매되고 있습니다.  
과일의 **재고는 10개씩**으로 동일합니다.

**장난감 가게**에는 미니언즈 피규어와 머리띠를 판매합니다.  
미니언즈 피규어는 **1000원** 머리띠는 **500원**에 판매가되고 있고 각각 **재고는 각각 10개**로 동일합니다.

**짱구**는 마을 주민입니다. 짱구는 **3000원의 용돈**이 있습니다.  
과일 가게에서 사과를 2개 구매하고 파인애플을 1개 구매한 후  
장난감 가게에서 미니언즈 피규어 1개 머리띠 1 개를 구매하려고 합니다.

물건을 다 산 후 짱구가 구매한 물품들을 나열하여 출력해주세요.  
또 남은 용돈을 얼마인지 계산하여 출력해주세요

### 풀이

먼저 가게를 만들 데이터들을 준비합니다.  
데이터에 따라 만들어지는 가게의 물건들이 달라지게 됩니다.

```javascript
var fruits = { // 과일가게를 만들 데이터
  apple: {
    price: 200,
    stock: 10
  },
  pineapple: {
    price: 500,
    stock: 10
  }
}

var toys = { // 장난감 가게를 만든 ㅔ이터
  minions: {
    price: 1000,
    stock: 10
  },
  teddyBear: {
    price: 500,
    stock: 10
  }
}
```

가게를 만들 생성자 함수를 정의합니다.  
생성자 함수는 가게의 이름과 판매할 아이템 데이터를 받습니다.

```javascript
function Shop(name, items) { // 가게이름, 아이템 데이터
  this.name = name;
  this.items = items;
}

// 위에서 만들어둔 fruits 데이터를 넣어 과일 가게를 생성합니다.
new Shop('과일 가게', fruits)
```

계속해서 생성자함수에 과일을 판매하는 함수를 만들겠습니다.  
**sellItem\( \)** 이라는 함수는 과일의 이름과 구매 수량을 매개변수로 받습니다.  
판매하고있는 items 에서 넘겨받은 이름을 가진 객체를 가져와 재고에서 구매한 수량만큼 뺴줍니다.

```javascript
function Shop(name, items) {
  this.name = name;
  this.items = items;
  /* 판매될 아이템이름과, 수량을 받는다 */
  this.sellItem = function(name, qauntity) { // 이름, 구매수량
    var item = this.items[name] // name 이라는 이름을 가진 객체를 가져옵니다.
    item.stock -= qauntity // 재고에서 구매수량만큼 빼줍니다.
    return { // 구매자가 지불해야될 가격과 구매한 아이템을 리턴해줍니다.
      itemName: item.name,
      price: item.price * qauntit
    };
  }
}
```

이제 구매자를 만들어 보려고 합니다 :\)  
유저를 만들 수 있는 생성자 함수를 만듭니다.

```javascript
function User(name, money) {
  this.name = name;
  this.money = money;
  this.receipt = [];
}
new User('olaf', 3000); // olaf 에게 3000원의 용돈을 줍니다.
```

User 는 과일을 구매할 수 있습니다.

```javascript
function User(name, money) {
  this.name = name;
  this.money = money;
  this.receipt = [];
  this.buyItem = function(item) { // buyItem 은 아이템 이름과, 구매한 가격을 받습니다.
    this.receipt.push(item.itemName); // 구매한 아이템은 영수증에 기록하고
    this.money -= item.price; // 구매를 위해 지불한 돈만큼 자신의 돈에서 차감합니다.
  }
}
```

이제 위에서 만든 것들을 잘 조합해서 사용하기만 하면됩니다.

```javascript
var fruitShop = new Shop('과일 가게', fruits); // 과일 가게 생성
var toyShop = new Shop('장난감 가게'); // 장난감 가게 생성
var user = new User('olaf', 5000);

var buyApple = fruitShop.sellItem('apple', 3) // 사과 3개를 구매하였습니다.
console.log('구매한 아이템', buyApple.itemName); // apple
console.log('지불해야되는 돈', buyApple.price); // 600
console.log('user가 사과를 구매했습니다.')

user.buyItem(buyApple); // olaf 가 가격을 지불합니다.
console.log('사과 구매 후 user 정보')
console.log('남은 용돈', user.money); // 남은 용돈 4400
console.log('영수증', user.receipt); // [ 'apple' ]

toyShop.sellItem('minions',  5); // 똑같이 장난감도 구매하면 되겠죠 :)
```

User 는 구매자의 역할이고 Shop 들은 판매하는 입장입니다.  
처음에는 이해하기 조금 어려울 수 있어요. 큰 흐름을 보려고하면 조금 더 이해가 수월할거에요

### 예외처리

프로그램을 만들보면 우리의 의도대로 동작하지 않는 경우가 분명히 발생합니다.

위의 코드에서 Shop 의 sellItem 을 예로 들어보겠습니다.  
sellItem 은 아이템의 이름과 수량을 받아서 판매를 하는 함수입니다. 그런데 가게의 아이템 재고보다 더 많은 수량을 구매자가 구매하길 원한다면 어떻게 될까요?

```javascript
this.sellItem = function(name, qauntity) { // 이름, 구매수량
    var item = this.items[name] // name 이라는 이름을 가진 객체를 가져옵니다.
    item.stock -= qauntity // 재고에서 구매수량만큼 빼줍니다.
    return { // 구매자가 지불해야될 가격과 구매한 아이템을 리턴해줍니다.
      itemName: item.name,
      price: item.price * qauntit
    };
 }
```

가게의 stock 은 - 가 되고 구매자는 수량대로 가격을 지불 하게됩니다. 그래서 우리는 재고보다 많은 수를 구매하고자 하면 구매를 막거나 현재 재고만큼 판매할 수 있도록 예외처리를 해줘야합니다.

```javascript
this.sellItem = function(name, qauntity) { // 이름, 구매수량
    var item = this.items[name] // name 이라는 이름을 가진 객체를 가져옵니다.
    if (qauntity > item.stock) { // 구매하고자 하는 수량이 재고보다 많다면 
      var result = {
        itemName: name,
        price: item.price * item.stock // 현재있는 재고의 수량만큼 판매
      }
      item.stock = 0; // 재고를 0 으로 바꿔줘야겠죠 ?
      return result
    } else { // 구매하고자 하는 수량이 재고보다 작을 때 
      item.stock -= qauntity // 재고에서 구매수량만큼 빼줍니다.
      return { // 구매자가 지불해야될 가격과 구매한 아이템을 리턴해줍니다.
        itemName: name,
        price: item.price * qauntity
      };
    }
  }
```

User 의 buyItem 도 예외처리가 필요합니다.  
가진 용돈보다 과일의 구매 가격이 클 때 구매하지 못 하도록 예외처리를 해줘야합니다.

```javascript
this.buyItem = function(item) { // buyItem 은 아이템 이름과, 구매한 가격을 받습니다.
    if (item.price > this.money) { // 과일 가격이 용돈보다 클 경우 
      console.log('용돈이 부족합니다.');
      return;
    }
    this.receipt.push(item.itemName); // 구매한 아이템은 영수증에 기록하고    
    this.money -= item.price; // 구매를 위해 지불한 돈만큼 자신의 돈에서 차감합니다.  
 }
```

### 마무리

우리는 예제를 통해서 생성자 함수를 이용해 모듈화를 하는 방법과 모듈을 조합하여 사용하는 객체지향적방식 또 함수를 이용하는 방법을 알아보았습니다.

위의 예제를 이해했다면 뒤에서 배울 prototype, module pettern 등의 학습에도 무리 없을거라고 생각합니다.

