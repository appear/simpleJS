---
description: Coding convention 에 대해 학습합니다
---

# ESLint

## ES Lint 를 이용한 Convention

프로젝트 개발은 보통 여러사람이 진행하게됩니다.

그렇다보니 프로젝트의 전체적인 코드 패턴은 자연스럽게 달라지게됩니다.  
코드패턴이 달라지게되면 코드를 유지보수하거나 개발함에 있어 많은 혼란이옵니다.

이런 일을 방지하기 위해 코드 패턴에 대한 규칙을 정하게 되는데 이때 사용하는 것이 **ESLint** 입니다.타입크립트의 경우 TSLint 를 이용하게됩니다.

### 사용해보기

먼저 ESLint 를 설치합니다.

```bash
$ npm init -y
$ npx eslint --init
```

여러개의 선택지가 나옵니다. 저는 Standard lint 를 적용하겠습니다.

```text
How would you like to configure ESLint > Use a popular style guide
Which style guide do you want to follow? > Standard
What format do you want your config file to be in? > JavaScript
npm install now ? > Y
```

install Y 를 해주셔야 Standard Lint 를 적용하기 위한 모듈들을 자동으로 받아줍니다.

![.eslintrc](../.gitbook/assets/image%20%286%29.png)

.eslinrc 파일이 eslint 설정 파일입니다. 룰을 추가하거나 여러가지 option 들을 설정할 수 있습니다.

index.js 라는 파일을 만들고 아래의 코드를 추가해보겠습니다.

```javascript
// index.js
console.log("a");
```

그러면 아래와 같이 eslint 룰에 어긋나는 것들에 빨간 줄이 그어집니다.   
Standard 에서는 singlequote 를 사용하도록 권장하는데 doublequote 를 사용했기 때문에 나는 경고입니다.  


![](../.gitbook/assets/image%20%2817%29.png)

singlequote 로 수정한 후 기존 경고는 사라지고 새로운 경고가 나왔습니다. semicolon 을 지우라는 경고와 한줄의 공백을 두라는 경고입니다. 먼저 semicolon  을 제거해보겠습니다.

![](../.gitbook/assets/image%20%2822%29.png)

이제 하나의 경고만 남게되었습니다. 만약 이 경고를 무시하고 싶다거나 경고가 아닌 에러의 level 로 올리고 싶다면 .eslintrc 에서 rule 을 설정해주면됩니다.

![](../.gitbook/assets/image%20%284%29.png)

아래와 같이 해당 rule 의 level 을 0 으로 만들게되면 lint 는 이 rule 에 관해서는 신경쓰지 않습니다.

```javascript
module.exports = {
    "extends": "standard",
    "rules": {
        "eol-last": 0   
    }
};
```

### Scripts 를 이용하여 lint 검사

다시 doublequote 로 변경하여 lint rule 에 어긋나게 만들어보겠습니다.

```javascript
console.log("a")
```

```bash
$ npx eslit "*.js"
```

위의 명령어를 이용하여 lint 검사 결과를 알 수 있습니다.

![](../.gitbook/assets/image%20%2814%29.png)

```bash
$ npx eslint '*.js' --fix
```

--fix 옵션을 이용하면 검사와 동시에 자동으로 lint rule 에 맞는 코드로 변경해줍니다.

### prettier, vs code 를 이용하여 좀 더 편하게 개발하기

따로 --fix 처리를 해주지 않아도 prettier 와 vscode 를 이용하면 저장과 동시에 코드를 lint rule 에 맞게 변경할 수 있습니다.

```bash
$ npm install -D prettier
$ npm install -D eslint-config-prettier eslint-plugin-prettier
```

.eslintrc 에 plugin 을 추가합니다 .

```javascript
module.exports = {
    "extends": "standard",
    "plugins": ["prettier"],
    "rules": {
        "eol-last": 0   
    }
};
```

VS code 마켓에서 prettier 플러그인을 설치해주세요

![](../.gitbook/assets/image%20%289%29.png)

설치후 VS code 작업영역 설정 부분에 아래의 설정을 작성합니다.  
윈도우의 경우 ctrl + , Mac 의 경우 Cmd + ,

```javascript
{
  "editor.formatOnSave": true,
  "javascript.format.enable": false,
  "prettier.eslintIntegration": true
}
```

이제 코드를 저장할 때 마다 lint rule 에 따라 자동으로 수정됩니다.

