---
layout: single
title:  "Innovation Camp JavaScript 과제 (day10)"
categories: JavaScript
toc: true
sidebar: 
    nav: "docs"
---

<img src="https://velog.velcdn.com/images/danchoi/post/1cf256b0-1ff4-4f55-b594-50810cfae109/image.jpeg" alt="post-thumbnail" style="zoom:80%;" />

<aside>
🐤 JavaScript의 자료형과 JavaScript만의 특성은 무엇일까 ?
</aside>

- 느슨한 타입(loosely typed)의 동적(dynamic) 언어

  
```js
JavaScript는 느슨한 타입(loosely typed)의 동적(dynamic) 언어입니다. 
JavaScript의 변수는 어떤 특정 타입과 연결되지 않으며, 
모든 타입의 값으로 할당 (및 재할당) 가능합니다.

let foo = 42 // foo가 숫자
foo = 'bar' // foo가 이제 문자열
foo = true // foo가 이제 불리언
```  


- JavaScript 형변환
[w3school의 형변환](https://www.w3schools.com/js/js_type_conversion.asp) 관련자료를 참고해 보자.
- ==, ===
[비교 연산자(w3school)](https://www.w3schools.com/js/js_comparisons.asp)
[비교 연산자2(TCPschool)](http://www.tcpschool.com/javascript/js_operator_comparison)
- 느슨한 타입(loosely typed)의 동적(dynamic) 언어의 문제점은 무엇이고 보완할 수 있는 방법에는 무엇이 있을지 생각해보세요.
  
```
JavaScript는 느슨한 타입의 동적 언어이기 때문에 
(변수 생성 시)원시 변수의 타입을 미리 선언하지 않아도 된다는 장점이 있다.
하지만 많은 기능 명세서와 API가 오고 가는 대형프로젝트(혹은 협업 시)에서 
타입이 올바른지 체크하는 것이 굉장히 까다롭기 때문에 배포 시 
예상치 못한 문제와 직면할 수 있다.

실행 도중에 변수에 예상치 못한 타입이 들어와 타입에러가 발생할 수 있음

동적타입 언어는 런타임 시 확인할 수 밖에 없기 때문에, 
코드가 길고 복잡해질 경우 타입 에러를 찾기가 어려워 집니다.

이러한 불편함을 해소하기 위해  정적 타입 체크와 
강력한 문법을 추가한 TypeScipt나 Flow 등을 사용할 수 있습니다.
```

- undefined와 null의 미세한 차이들을 비교해보세요.


~~~
- undefined
변수를 선언하고 값을 할당하지 않은 상태이다.
자료형이 없는 상태이다.
- null
변수를 선언하고 빈 값을 할당한 상태(빈 객체)이다
~~~


<aside>
🐤 JavaScript 객체와 불변성이란 ?
</aside>

- 기본형 데이터와 참조형 데이터
![](https://velog.velcdn.com/images/danchoi/post/6244d65e-fe7f-4b4b-ae92-b8ef57693ac3/image.png)
```
1. Primitive Type (원시타입)
원시 타입의 데이터는 변수에 할당이 될 때 메모리 상에 
고정된 크기로 저장이 되고 해당 변수가 원시 데이터 값을 보관한다. 
원시 타입 자료형은 모두 변수 선언, 초기화, 할당 시 값이 
저장된 메모리 영역에 직접적으로 접근한다. 
즉, 변수에 새 값이 할당이 될 경우, 변수에 할당된 메모리 블럭에 
저장된 값을 바로 변경한다.

2. Reference Type (참조 타입)
참조 타입의 데이터는 크기가 정해져 있지 않고 변수에 할당이 될 때 
값이 직접 해당 변수에 저장될 수 없으며 변수에는 데이터에 대한 
참조만 저장된다. 
변수의 값이 저장된 힙 메모리의 주소값을 저장한다. 
참조 타입은 변수의 값이 저장된 메모리 블럭의 주소를 가지고 있고 
자바스크립트 엔진이 변수가 가지고 있는 메모리 주소를 이용해서 
변수의 값에 접근한다.
```

출처: https://velog.io/@surim014/JavaScript-Primitive-Type-vs-Reference-Type
- JavaScript 형변환

- 불변 객체를 만드는 방법
[Object.freeze()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)
- 얕은 복사와 깊은 복사
[Swallow copy](https://developer.mozilla.org/en-US/docs/Glossary/Shallow_copy)
[Deep copy](https://developer.mozilla.org/en-US/docs/Glossary/Deep_copy)

<aside>
🐤 호이스팅과 TDZ는 무엇일까 ?
</aside>

- [스코프](https://developer.mozilla.org/ko/docs/Glossary/Scope), [호이스팅](https://developer.mozilla.org/ko/docs/Glossary/Hoisting), [TDZ](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/let#시간상_사각지대)
- 함수 선언문과 함수 표현식에서 호이스팅 방식의 차이


```
호이스팅

호이스팅(Hoisting)의 사전적 의미는 끌어 올리다 라는 뜻을 가지고 있다.
여기서도 같은 의미로 쓰인다. 함수 안에 있는 변수나 함수 맨위로 끌어올린다는 것이다.

실제로 코드가 끌어올려지는 것은 아니며, 
자바스크립트 Parser가 내부적으로 끌어올려서 처리한다.

호이스팅 대상

var 와 함수 선언문 이 호이스팅 대상이다.
let 또는 const 그리고 함수 표현식은 해당되지 않는다.
```


출처: https://velog.io/@hyun-jii/함수선언문-함수표현식과-호이스팅

- 여러분이 많이 작성해온 let, const, var, function 이 어떤 원리로 실행되는지 알 수 있어요.
- [실행 컨텍스트와 콜 스택](https://medium.com/sjk5766/call-stack과-execution-context-를-알아보자-3c877072db79)
- 스코프 체인, 변수 은닉화


<aside>
🐤 실습 과제
</aside>

- 콘솔에 찍힐 b 값을 예상해보고, 어디에서 선언된 “b”가 몇번째 라인에서 호출한 console.log에 찍혔는지, 왜 그런지 설명해보세요.
  주석을 풀어보고 오류가 난다면 왜 오류가 나는 지 설명하고 오류를 수정해보세요.
  
  
  
```jsx
let b = 1;

function hi () {

  const a = 1;

  let b = 100;

  b++;

  console.log(a,b);

}

//console.log(a); 선언되어있지 않기 때문에 오류가 발생

console.log(b);

hi();

console.log(b);

//1
//1, 101
//1
```
