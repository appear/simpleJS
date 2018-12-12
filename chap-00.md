---
description: 자바스크립트의 역사와 간단한 동작원리를 알아봅니다.
---

# 자바스크립트란?

![](.gitbook/assets/body%20%282%29.png)

## 자바스크립트란 ? <a id="&#xC790;&#xBC14;&#xC2A4;&#xD06C;&#xB9BD;&#xD2B8;&#xB780;"></a>

웹 페이지는 기본적으로 다음과 같은 요소들로 이루어져 있습니다.

* [HTML](https://developer.mozilla.org/ko/docs/Learn/HTML/Introduction_to_HTML/Getting_started) : HTML을 통하여 페이지를 어떻게 브라우저에 보여줄지 구조를 잡습니다.
* [CSS](https://developer.mozilla.org/ko/docs/Web/CSS/시작하기/CSS란) :  구조를 잡은 것을 어떻게 보여줄지 스타일을 입혀줍니다. \(크기, 색상 위치 등\) 
* [JAVASCRIPT](https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps/What_is_JavaScript) :  HTML & CSS 로 만들어진 정적인 페이지를 동적으로 동작할 수 있게 만들어줍니다. \(Slide, Drag&drop 등\)

### 자바스크립트에 영향을 준 언어 <a id="&#xC790;&#xBC14;&#xC2A4;&#xD06C;&#xB9BD;&#xD2B8;&#xC5D0;-&#xC601;&#xD5A5;&#xC744;-&#xC900;-&#xC5B8;&#xC5B4;"></a>

자바스크립트의 프로그래밍 스타일은 함수형 프로그래밍과 객체지향 프로그래밍을 함께 사용합니다.

* 자바 : 문법, ‘원시 값 vs 객체 관계’
* 스키마와 오크 : 함수
* 셀프 : 프로토타입 상속
* 펄과 파이썬 : 문자열과 배열, 정규표현식

### 역사 <a id="&#xC5ED;&#xC0AC;"></a>

초기의 자바스크립트는 웹페이지의 보조적 기능을 수행하기 위한 용도로 사용되었었습니다. 중요한 로직들은 서버사이드에서 처리를 하고 클라이언트단에서는 받은 데이터 또는 HTML등을 렌더링 해주는 수준이었습니다.  
JQuery 같은 라이브러리의 등장으로 DOM을 쉽게 다룰 수 있어졌고, 브라우저엔진과 웹의 발전으로 서버사이드에서 하던일들의 많은 부분들을 클라이언트단으로 이동되었습니다.

* 1997년 : DOM 제어를 이용하여 컨텐츠와 스타일의변화를 주는 것이 가능해졌다. IE4와 넷스케이프 등 동적 HTML제어가 등장하였습니다.
* 1999년 : IE5에서 서버요청을 보내고 텍스트형식의 데이터를 받는것이 가능해졌습니다.
* 2001년 : 더글락스 크락포드는 텍스트 형식으로 데이터를 저장하는 문법을 [JSON](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON)이라 칭하고 문서화했습니다.
* 2005년 : 비동기 방식의 **Ajax**의 등장 대표적으로 Google Maps가 있다. **Ajax** 등장이후 **JSON**이 인기를 끌기시작했습니다. 결과적으로 **DOM**을 다룰일이 많아졌습니다.
* 2006년 : DOM을 간편하게 할 수 있도록 **JQuery**가 API를 제공하여 Javascript 에게 날개를 달아 주는 시기였습니다.
* 2007년 : 애플이 [WebKit](https://ko.wikipedia.org/wiki/웹킷)엔진을 소개하였습니다. WebKit은 안드로이드의 메인 엔진이고, iOS의 유일한 엔진으로 모바일 시장을 지배하고 있습니다.
* 2008년 : 구글 크롬 [**V8**](https://ko.wikipedia.org/wiki/크롬_V8)엔진의 등장으로 자바스크립트의 느리다는 인식을 바꿔주는 큰 발전이있었습니다.
* 2009년 : **Node.js**의 등장 서버사이드언어를 자바스크립트로 구성할 수 있게되었습니다.

### 브라우저의 동작원리 <a id="&#xB3D9;&#xC791;&#xC6D0;&#xB9AC;"></a>

유저가 www.naver.com 등 URL 을 입력하게 되면, 해당 웹 페이지의 리소스를 서버에 요청하고 브라우저는 서버로부터 Html, CSS, Javascript 파일을 응답 받아 우리가 보는 화면을 그려줍니다. \(크롬 개발자도구의 Network 탭을 보시면 확인 가능합니다\)

사실 좀더 많은 일들이 일어나는데 간단하게 설명해보겠습니다.

1. 먼저 Html, CSS 파일은 **HTML 파서**를 통해 **DOM Tree**를 만들어 집니다. 뒤에서 배우겠지만 DOM 에 접근하기 위해서는 **document** 라는 객체로 접근을 하게되는데 이때 **document** 의 접근이 가능한 이유가 **DOM Tree** 가 만들어 졌기 때문입니다. HTML 파서는 **Script태그**를 만나면 DOM 생성 프로세스를 **중지**하고 **자바스크립트 엔진**에게 제어권한을 넘깁니다. 태그 위치에 따라 DOM 생성이 지연될 수 있습니다.  **\(이와 같은 동작방식 때문에 &lt;/Body&gt; 태그 바로 위쪽에 Script 태그를 붙이는 것 입니다\)**
2. CSS 같은 경우 **CSS 파서**에 의해 파싱되어 CSS Object Model 트리가 만들어집니다 \([https://developer.mozilla.org/ko/docs/Web/API/CSS\_Object\_Model](https://developer.mozilla.org/ko/docs/Web/API/CSS_Object_Model)\)
3. 하지만 DOM Tree 만으로는 렌더링을 할 수 없습니다. 우리가 보고있는 면을 만들기 위해서는 **렌더링 트리**라는 것이 필요합니다. 위에서 만들어진 **DOM Tree** 와 **CSSOM** 을 바탕으로 렌더링 트리가 구성됩니다. \(이때 CSSOM 을 바탕으로 화면에 배치가 이루어지고 색상 등 스타일이 입혀집니다. **redraw & repaint** 가 일어납니다\)
4. 비로소 우리가 화면을 볼 수 있게 됩니다.

![&#xBE0C;&#xB77C;&#xC6B0;&#xC800;&#xC758; &#xB3D9;&#xC791; &#xBC29;&#xC2DD; \(&#xCD9C;&#xCC98;: http://d2.naver.com/helloworld/59361\)](https://d2.naver.com/content/images/2015/06/helloworld-59361-3.png)

* **브라우저동작원리** : [http://d2.naver.com/helloworld/59361](http://d2.naver.com/helloworld/59361)
* **WebKit 구동원리** : [http://rtcc.hanyang.ac.kr/sitedata/2015\_2\_ISP/howbrowserswork\_20150915.pdf](http://rtcc.hanyang.ac.kr/sitedata/2015_2_ISP/howbrowserswork_20150915.pdf)

### 인터프리터 <a id="&#xC778;&#xD130;&#xD504;&#xB9AC;&#xD2B8;"></a>

자바스크립트는 인터프리터 동작 방식의 언어다 라는 말을 들어보신적 있으신가요 ?

> **인터프리터란 ?**  
>   
> 전체를 컴파일하여 실행하는 것이 아닌, 위에서부터 아래로 순차적으로 실행하며 코드를 한줄 한줄 기계어로 변환해가며 실행하는 방식을 인터프리터라고합니다.

그렇다면 컴파일 언어와 인터프리터 언어의 차이점은 무엇일까요 ?

**컴파일 언어**는 최초 실행시 작성된 모든 코드를 컴파일 합니다. 그렇기 때문에 최초 실행시 속도가 느리다는 특징이 있으나 컴파일 된 후에는 따로 컴파일을 거칠 필요가 없기 때문에 빠른 속도를 보입니다.

**인터프리터**의 경우 이런 컴파일 과정을 거치지 않기 때문에 최초 빠른 속도를 보입니다. 하지만 한줄 한줄 컴파일을 해야되기 때문에 효율성이 떨어질 수 있습니다.

자바스크립트는 인터프리터 방식의 언어였습니다. 하지만 모던 자바스크립트는 JIT 라는 컴파일 방식을 채택하였습니다.

> **JIT\(Just-In-Time\) 컴파일이란?**  
>   
> 컴파일\(코드를 기계어로 변환해주는 과정\) + 인터프리터방식입니다.  
> Just-In-Time 말 그대로 그 순간 즉, 프로그램 실행시점에 필요한 부분을 바로 컴파일하는 동적 컴파일 방식입니다. 기존 인터프리터방식보다 빠른 실행속도를 보여줍니다.  
> 하지만 JIT 컴파일링은 실행될 때 최초 실행되기 때문에, 최초 실행에서는 조금 느릴 수 있습니다.

