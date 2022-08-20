--- 
layout: single 
title:  "[React] react-router-dom Error (day18)" 
categories: React
tags: react
toc: true
sidebar: 
    nav: "main"
---

![post-thumbnail](https://velog.velcdn.com/images/danchoi/post/eeec7075-0869-4c27-9be0-2f9d2be12af3/image.jpeg)

```
npm install react-router-dom 
```
실행 후 신나게 라우팅에 대해 실습을 하려다 보니

모니터 속의 localhost:3000에는 흰화면만 지속되었다.
콘솔창을 켜보니 오류들로 빨갛게 물들어 있었다.
![](https://velog.velcdn.com/images/danchoi/post/7630c80c-4a1c-495b-a1ad-79d5fe323f01/image.png)

~~~
Uncaught Error: A <Route> is only ever to be used as the child of <Routes> element, never rendered directly. Please wrap your <Route> in a <Routes>.
    at invariant (router.ts:5:1)
    at Route (components.tsx:147:1)
    at renderWithHooks (react-dom.development.js:16305:1)
    at mountIndeterminateComponent (react-dom.development.js:20074:1)
    at beginWork (react-dom.development.js:21587:1)
    at HTMLUnknownElement.callCallback (react-dom.development.js:4164:1)
    at Object.invokeGuardedCallbackDev (react-dom.development.js:4213:1)
    at invokeGuardedCallback (react-dom.development.js:4277:1)
    at beginWork$1 (react-dom.development.js:27451:1)
    at performUnitOfWork (react-dom.development.js:26557:1)
~~~

콘솔에 나와있는 내용대로 < Route > 태그를 < Routes >태그로 감싸줘봤지만 여전히 해결되지 않았기 때문에 구글 검색을 통해 원인을 발견하게 되었다.
react-router-dom 라이브러리가 버전업데이트 됨에 따라서
< Route >의 매개변수 이름이 변경되었다고 한다.
그렇기 때문에 해결책은

1. 최신버전에 맞게 작성을 하거나  

```jsx
<Routes>
<Route path="/" element={<Home/>}/>
</Routes>
```  

2. 이전 버전을 설치하여 사용해야 한다.

출처: https://developer-ping9.tistory.com/214
