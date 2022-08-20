---
layout: single
title:  "Innovation Camp Algorithm feat.Programmers (day6)"
categories: algorithm
---
[repository](https://github.com/dan-studio/algorithms)


알고리즘 둘째 날 
토요일인데 날씨가 너무 좋네.
알고리즘은 어렵네.

### 10.행렬의 덧셈


~~~
문제 설명

행렬의 덧셈은 행과 열의 크기가 같은 두 행렬의 같은 행, 같은 열의 값을 
서로 더한 결과가 됩니다. 
2개의 행렬 arr1과 arr2를 입력받아, 행렬 덧셈의 결과를 반환하는 함수, 
solution을 완성해주세요.

제한 조건
행렬 arr1, arr2의 행과 열의 길이는 500을 넘지 않습니다.
~~~


점점 문제가 어려워진다. 이것 또한 오래 잡고 있었다.
[for문](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for)을 통해 해결을 할 수 있지만


~~~js
//for
function solution(arr1, arr2){
  let answer = []
  for(let i=0; i<arr1.length; i++){
    let tmp = []
    for(let j=0; j<arr1[i].length; j++){
    	tmp.push(arr1[i][j]+arr2[i][j])
    }
    answer.push(tmp)
  }
  return answer
}
~~~


[map()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)메서드를 통해 조금 더 간결한 코드로 해결을 할 수 있기도 하다.
~~~js
const solution = (arr1, arr2)=>{
  return arr1.map((val,idx)=>val.map((val_val, val_idx)=>val_val+arr2[idx][val_idx]))
}
~~~

### 11. x만큼 간격이 있는 n개의 숫자


```
문제 설명
함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 
x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 
다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

제한 조건
x는 -10000000 이상, 10000000 이하인 정수입니다.
n은 1000 이하인 자연수입니다.
```

```js
function solution(x,n){
  var answer = [];
  for(let i = 1; i<=n; i++){ //for문을 돌려 i를 n의 값만큼 1씩 증가시켜 x에 곱한 값을 answer 배열에 넣어준다.
   answer.push(x*i)
  }
  return answer
}
```

### 12. 부족한 금액 계산하기


~~~
문제 설명
새로 생긴 놀이기구는 인기가 매우 많아 줄이 끊이질 않습니다. 
이 놀이기구의 원래 이용료는 price원 인데, 놀이기구를 N 번 째 이용한다면 
원래 이용료의 N배를 받기로 하였습니다. 
즉, 처음 이용료가 100이었다면 2번째에는 200, 3번째에는 300으로 요금이 인상됩니다.
놀이기구를 count번 타게 되면 현재 자신이 가지고 있는 금액에서 
얼마가 모자라는지를 return 하도록 solution 함수를 완성하세요.
단, 금액이 부족하지 않으면 0을 return 하세요.

제한사항
놀이기구의 이용료 price : 1 ≤ price ≤ 2,500, price는 자연수
처음 가지고 있던 금액 money : 1 ≤ money ≤ 1,000,000,000, 
money는 자연수
놀이기구의 이용 횟수 count : 1 ≤ count ≤ 2,500, count는 자연수
~~~
~~~js
function solution(price, money, count) {
  let totalPrice = 0;
  
  for(let i=1;i<=count;i++){
      totalPrice += price * i;//for문으로 i의 값을 count의 값만큼 1씩 증가시켜주고 totalPrice의 값에 price에 i만큼 곱한 값을 전무 더해줍니다.
  }
  
  return money > totalPrice ? 0 : totalPrice-money
  //삼항연산자를 사용해 money의 값이 totalPrice보다 작을 경우 totalPrice에서 money를 뺀 값을 반환해 줍니다.
}
~~~
