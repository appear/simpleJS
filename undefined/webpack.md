# Webpack

### webpack

웹팩은 프로젝트의 구조를 분석하고 자바스크립트 모듈을 비롯한 관련 리소스들을 찾은 다음 이를 브라우저에서 이용할 수 있는 번들로 묶고 패킹하는 모듈 번들러\(Module bundler\)다.

```text
npm i -g webpack webpack-cli webpack-dev-server // bundle
npm i -D webpack // config
```

**webpack.config.js**

```javascript
const path = require("path");
const webpack = require("webpack");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: {
    modules: "./modules.js"
  },
  module: {},
  resolve: {
    extensions: ["*", ".js"] // 확장자를 생략할 수 있도록
  },
  output: {
    filename: "[name].bundle.js", // bundle 될 파일 이름
    path: path.resolve(__dirname, "dist"), // 위치
    publicPath: "/"
  },
  devServer: {
    contentBase: "./dist"
  },
  plugins: [
    new HtmlWebpackPlugin({
      title: "Development",
      template: "./index.html",
      filename: "./index.html",
      showErrors: true // 에러 발생시 메세지가 브라우저 화면에 노출 된다.
    })
  ]
};
```

### babel

babel 이란 우리가 작성한 ES6 또는 ES7 코드를 ES5 코드로 transfile 하기 위한 도구입니다.  
babel v7 부터는 @babel이라는 네임스페이스 안에 패키지들이 들어가도록 되었습니다.

```text
npm i -D babel-loader @babel/core @babel/preset-env
```

```text
rules: [
  {
    test: /\.(js)$/,
    exclude: /node_modules/,
    use: ['babel-loader']
  }
],
```

**.babelrc**

`package.json` 에 바로 babel 설정값을 추가해 줄 수 있지만, `.babelrc` 라는 파일을 따로 구성하여 설정하겠습니다.  
`Babel` 은 다양한 module 들로 구성되어져 있는데 presets 는 특정 기능을하는 modules 의 모음입니다. 어떤 버전\(ES5\) 으로 컴파일할지에 대한 정보를 적어줄 수 있습니다.

ex. babel-presets-es2015 -&gt; @babel/preset-env \(es5 로 컴파일\)

```javascript
{
  "presets": ["@babel/preset-env"]
}
```

### css

css file 들도 사용할 것 이기 때문에 loader 를 추가해줍니다.

```text
npm i -D css-loader style-loader
```

```javascript
rules: [
  {
    test: /\.css$/,
    use: ["style-loader", "css-loader"]
  }
];
```

### html plugin

bundle file 이름은 매번 달라질 수 있습니다. html 의 js 들의 파일 이름을 매번 변경해주기에는 많은 귀찮음이 따릅니다. `html-webpack-plugin` 을 사용하여 문제를 해결할 수 있습니다.

```text
npm i -D html-webpack-plugin
```

```javascript
plugins: [
  new HtmlWebpackPlugin({
    title: "dev",
    template: "./index.html", // 대상 html
    filename: "./index.html", // bundle 될 file 과 위치
    showErrors: true // 에러 발생시 메세지가 브라우저 화면에 노출 된다.
  })
];
```

### scripts

실행과 build 를 쉽게 사용하기 위해 `package.json`에 명령어를 등록할 수 있습니다.

```javascript
"scripts": {
    "dev": "webpack-dev-server --config ./webpack.config.js --mode development --hot --inline",
    "build": "webpack",
    "watch": "webpack --watch"
  },
```

위의 설정해둔 scripts 로 빌드 또는 dev-server 를 실행할 수 있습니다.

```text
npm run dev
npm run build
```

