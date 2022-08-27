---
layout: single
title:  "[JavaScript] Synchronous and Asynchronous (day27)" 
subtitle: "about Synchronous and Asynchronous"
createDate: "2022-08-27"
categories: javascript
tags: javascript
header:
  teaser: "/assets/images/JS.jpeg"
---

![img](https://velog.velcdn.com/images/danchoi/post/b968693b-1029-4afc-97ef-1f81ef174c61/image.jpeg)

동기(Synchronous)

- 응답을 받고 다음 프로세스를 실행
- 순차적으로 처리하기 때문에 비동기에 비해 느리다.
- 디버깅이 쉽다

비동기(Asynchronous)

- 응답에 상관 없이 바로 다음 프로세스 진행
- 여러가지 로직이 동시에 처리됨.
- 빠른 결과 도출
- 다른 프로세스의 결과 값을 받아 쓸때 이를 조절해야함.

비동기 처리 방식의 문제점을 해결하기 위해서는 콜백 함수(callbackFunction)를 이용할 수 있다.