---
layout: single
title:  "[JavaScript] Optional Chaining (day23)" 
subtitle: "about optional chaining"
createDate: "2022-08-23"
categories: javascript
tags: javascript
header:
  teaser: "/assets/images/JS.jpeg"
---

![img](https://velog.velcdn.com/images/danchoi/post/81cdc29c-395e-4b43-856a-d4be51de2af5/image.jpeg)

# [Optional chaining](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

**optional chaining** 연산자 (**`?.`**) 는 체인의 각 참조가 유효한지 명시적으로 검증하지 않고, 연결된 객체 체인 내에 깊숙이 위치한 속성 값을 읽을 수 있다.

```js
const adventurer = {
  name: 'Alice',
  cat: {
    name: 'Dinah'
  }
};

const dogName = adventurer.dog?.name;
console.log(dogName);
// expected output: undefined

console.log(adventurer.someNonExistentMethod?.());
// expected output: undefined
```

## 옵셔널 체이닝이 필요한 이유

사용자가 여러 명 있는데 그중 몇 명은 주소 정보를 가지고 있지 않다고 가정해봅시다. 이럴 때 `user.address.street` 를 사용해 주소 정보에 접근하면 에러가 발생할 수 있습니다.

```js
let user = {}; // 주소 정보가 없는 사용자

alert(user.address.street); // TypeError: Cannot read property 'street' of undefined
```

또 다른 사례론 브라우저에서 동작하는 코드를 개발할 때 발생할 수 있는 문제가 있습니다. 자바스크립트를 사용해 페이지에 존재하지 않는 요소에 접근해 요소의 정보를 가져오려 하면 문제가 발생하죠

```jsx
// querySelector(...) 호출 결과가 null인 경우 에러 발생
let html = document.querySelector('.my-element').innerHTML;
```

명세서에 `?.`이 추가되기 전엔 이런 문제들을 해결하기 위해 `&&` 연산자를 사용하곤 했습니다.

예시:

```jsx
let user = {}; // 주소 정보가 없는 사용자

alert( user && user.address && user.address.street ); // undefined, 에러가 발생하지 않습니다.
```

`let user = {}; // 주소 정보가 없는 사용자

alert(user.address.street); // TypeError: Cannot read property 'street' of undefined`

중첩 객체의 특정 프로퍼티에 접근하기 위해 거쳐야 할 구성요소들을 AND로 연결해 실제 해당 객체나 프로퍼티가 있는지 확인하는 방법을 사용했었죠. 그런데 이렇게 AND를 연결해서 사용하면 코드가 아주 길어진다는 단점이 있습니다.

## 옵셔널 체이닝의 등장

`?.`은 `?.`'앞’의 평가 대상이 `undefined`나 `null`이면 평가를 멈추고 `undefined`를 반환합니다.

**설명이 장황해지지 않도록 지금부턴 평가후 결과가 `null`이나 `undefined`가 아닌 경우엔 값이 ‘있다’ 혹은 '존재한다’라고 표현하겠습니다.**

이제 옵셔널 체이닝을 사용해 `user.address.street`에 안전하게 접근해봅시다.

```jsx
let user = {}; // 주소 정보가 없는 사용자

alert( user?.address?.street ); // undefined, 에러가 발생하지 않습니다.
```

`user?.address`로 주소를 읽으면 아래와 같이 `user` 객체가 존재하지 않더라도

에러가 발생하지 않습니다.

```jsx
let user = null;

alert( user?.address ); // undefined
alert( user?.address.street ); // undefined
```

위 예시를 통해 우리는 `?.`은 `?.` ‘앞’ 평가 대상에만 동작되고, 확장은 되지 않는다는 사실을 알 수 있습니다.

참고로 위 예시에서 사용된 `user?.`는 `user`가 `null`이나 `undefined`인 경우만 처리할 수 있습니다.

`user`가 `null`이나 `undefined`가 아니고 실제 값이 존재하는 경우엔 반드시 `user.address` 프로퍼티는 있어야 합니다. 그렇지 않으면 `user?.address.street`의 두 번째 점 연산자에서 에러가 발생합니다.

**옵셔널 체이닝을 남용하지 마세요.**

`?.`는 존재하지 않아도 괜찮은 대상에만 사용해야 합니다.

사용자 주소를 다루는 위 예시에서 논리상 `user`는 반드시 있어야 하는데 `address`는 필수값이 아닙니다. 그러니 `user.address?.street`를 사용하는 것이 바람직합니다.

실수로 인해 `user`에 값을 할당하지 않았다면 바로 알아낼 수 있도록 해야 합니다. 그렇지 않으면 에러를 조기에 발견하지 못하고 디버깅이 어려워집니다.

**`?.`앞의 변수는 꼭 선언되어 있어야 합니다.**

변수 `user`가 선언되어있지 않으면 `user?.anything` 평가시 에러가 발생합니다.

```javascript
// ReferenceError: user is not defined
user?.address;
```

`user?.anything`을 사용하려면 `let`이나 `const`, `var`를 사용해 `user`를 정의해야 하죠. 이렇게 옵셔널 체이닝은 선언이 완료된 변수를 대상으로만 동작합니다.



출처: https://ko.javascript.info/optional-chaining

