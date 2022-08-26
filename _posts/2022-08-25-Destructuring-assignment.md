---
layout: single
title:  "[JavaScript] Destructuring Assignment (day25)" 
subtitle: "about Destructuring assignment (구조 분해 할당)"
createDate: "2022-08-25"
categories: javascript
tags: javascript
header:
  teaser: "/assets/images/JS.jpeg"
---

![img](https://velog.velcdn.com/images/danchoi/post/b968693b-1029-4afc-97ef-1f81ef174c61/image.jpeg)

# 구조 분해 할당

**구조 분해 할당** 구문은 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript 표현식입니다.

```js
var a, b, rest;
[a, b] = [10, 20];
console.log(a); // 10
console.log(b); // 20

[a, b, ...rest] = [10, 20, 30, 40, 50];
console.log(a); // 10
console.log(b); // 20
console.log(rest); // [30, 40, 50]

({ a, b } = { a: 10, b: 20 });
console.log(a); // 10
console.log(b); // 20


// Stage 4(finished) proposal
({a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40});
console.log(a); // 10
console.log(b); // 20
console.log(rest); // {c: 30, d: 40}
```



## [배열 분해하기](https://ko.javascript.info/destructuring-assignment#ref-420)

배열이 어떻게 변수로 분해되는지 예제를 통해 살펴봅시다.

```javascript
// 이름과 성을 요소로 가진 배열
let arr = ["Daniel", "Choi"]

// 구조 분해 할당을 이용해
// firstName엔 arr[0]을
// lastName arr[1]을 할당하였습니다.
let [firstName, lastName] = arr;

alert(firstName); // Daniel
alert(lastName);  // Choi
```

### ['…'로 나머지 요소 가져오기](https://ko.javascript.info/destructuring-assignment#ref-421)

배열 앞쪽에 위치한 값 몇 개만 필요하고 그 이후 이어지는 나머지 값들은 한데 모아서 저장하고 싶을 때가 있습니다. 이럴 때는 점 세 개 `...`를 붙인 매개변수 하나를 추가하면 ‘나머지(rest)’ 요소를 가져올 수 있습니다.

```javascript
let [name1, name2, ...rest] = ["Son", "Salah", "Ronaldo", "Kane"];

alert(name1); // Son
alert(name2); // Salah

// `rest`는 배열입니다.
alert(rest[0]); // Ronaldo
alert(rest[1]); // Kane
alert(rest.length); // 2
```

### [나머지 패턴 ‘…’](https://ko.javascript.info/destructuring-assignment#ref-424)

나머지 패턴(rest pattern)을 사용하면 배열에서 했던 것처럼 나머지 프로퍼티를 어딘가에 할당하는 게 가능합니다. 참고로 모던 브라우저는 나머지 패턴을 지원하지만, IE를 비롯한 몇몇 구식 브라우저는 나머지 패턴을 지원하지 않으므로 주의해서 사용해야 합니다. 

```javascript
let options = {
  title: "Menu",
  height: 200,
  width: 100
};

// title = 이름이 title인 프로퍼티
// rest = 나머지 프로퍼티들
let {title, ...rest} = options;

// title엔 "Menu", rest엔 {height: 200, width: 100}이 할당됩니다.
alert(rest.height);  // 200
alert(rest.width);   // 100
```

출처: https://ko.javascript.info/destructuring-assignment

​		https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment