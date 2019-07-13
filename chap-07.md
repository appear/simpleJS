---
description: '여태까지 배운 내용들을 이용하여 과일가게와 장난감가게를 만들어봐요 :)'
---

# 실습\) 과일가게

![body](.gitbook/assets/body%20%282%29.png)

## 과일가게

### 문제

한 마을에는 **과일 가게**와 **장난감 가게**가 있습니다.  
**과일 가게**에는 사과와 파인애플을 팔며 **사과**는 **200원**, **파인애플**은 **500원**에 판매되고 있습니다.  
과일의 **재고는 10개씩**으로 동일합니다.  
  
또 남은 용돈을 얼마인지 계산하여 출력해주세요

### 풀이

먼저 가게를 만들 데이터들을 준비합니다.  
데이터에 따라 만들어지는 가게의 물건들이 달라지게 됩니다.

```javascript
var fruits = { // 과일가게를 만들 데이터
  apple: {
    name: '사과',
    price: 200,
    stock: 10
  },
  pineapple: {
    name: '파인애플',
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
function Shop(name, items) { // 가게이름, 아이템 데이터
  this.name = name;
  this.items = items;

  this.sell = function(name, qauntity) { // 이름, 구매수량
    var item = this.items[name] // name 이라는 이름을 가진 객체를 가져옵니다.

    if (!item) {
      console.log('찾으시는 과일이 없습니다.')
      return 
    }

    if(item.stock < qauntity) {
      console.log(`${item.name} 의 재고가 부족합니다.`)
      return 
    }

    return { // 구매자가 지불해야될 가격과 구매한 아이템을 리턴해줍니다.
      name: item.name,
      price: item.price * qauntity,
      qauntity: qauntity
    };
  }
  
  this.setStock = function(name, qauntity) {
    var item = this.items[name] 

    if (!item) {
      console.log('찾으시는 과일이 없습니다.')
      return 
    }

    item.stock = item.stock -= qauntity // 판매에 성공한 갯수만큼 재고를 빼줍니다.

    console.log(`${item.name} 의 재고가 ${item.stock} 으로 변경되었습니다`)
  }
}
```

이제 구매자를 만들어 보려고 합니다 :\)  
유저를 만들 수 있는 생성자 함수를 만듭니다.

```javascript
function User(name, money) {
  this.name = name;
  this.money = money;
}

new User('olaf', 5000); // olaf 에게 3000원의 용돈을 줍니다.
```

User 는 과일을 구매할 수 있습니다.

```javascript
function User(name, money) {
  this.name = name;
  this.money = money;
  
  this.buy = function(item) { // buyItem 은 아이템 이름과, 구매한 가격을 받습니다.
    
    if (this.money < item.price) {
      console.log(`${name} 을 구매하기에 돈이 부족합니다. 가격 :${item.price} 잔고: ${this.money}`)
      return 
    }

    this.money -= item.price; // 구매를 위해 지불한 돈만큼 자신의 돈에서 차감합니다.

    console.log(`${item.name} 을 구매하였습니다. 남은 돈: ${this.money}`)
    
    return {
      qauntity: item.qauntity // 구매를 성공한 수량을 리턴해줍니다.
    }
  }
}
```

이제 위에서 만든 것들을 잘 조합해서 사용하기만 하면됩니다.

```javascript
var fruitShop = new Shop('과일 가게', fruits); // 과일 가게 생성

var user = new User('olaf', 5000);

var sellInfo = fruitShop.sell('apple', 3) // 사과 3개를 구매하였습니다.

if (sellInfo) {
  console.log('구매한 아이템', sellInfo.name); // apple
  console.log('지불해야되는 돈', sellInfo.name); // 600
  
  const buyInfo = user.buy(sellInfo); // olaf 가 가격을 지불합니다.

  if(buyInfo) {
    fruitShop.setStock('apple', buyInfo.qauntity) // 재고를 조정합니다.
  }
}
```

User 는 구매자의 역할이고 Shop 들은 판매하는 입장입니다.  
처음에는 이해하기 조금 어려울 수 있어요. 큰 흐름을 보려고하면 조금 더 이해가 수월할거에요

### 마무리

우리는 예제를 통해서 생성자 함수를 이용해 모듈화를 하는 방법과 모듈을 조합하여 사용하는 객체지향적방식 또 함수를 이용하는 방법을 알아보았습니다.

위의 예제를 이해했다면 뒤에서 배울 prototype, module pettern 등의 학습에도 무리 없을거라고 생각합니다.

