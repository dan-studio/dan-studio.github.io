--- 
layout: single 
title:  "Innovation Camp Algorithm feat.Programmers (day10)" 
categories: algorithm
toc: true
sidebar: 
    nav: "docs"
---

### 16. 문자열 내 p와 y의 개수

~~~
문제 설명
대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.
예를 들어 s가 "pPoooyY"면 true를 return하고 "Pyy"라면 false를 return합니다.

제한사항
문자열 s의 길이 : 50 이하의 자연수
문자열 s는 알파벳으로만 이루어져 있습니다.
~~~
사용한 메서드:
[split()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/split)
[toUpperCase()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase)
[filter()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
~~~js
function solution(s){
  var split = s.toUpperCase().split('') //대소문자 구분 없이 해당 문자의 개수를 구해야 하므로 대문자로 변환을 해주었다.
  var p = split.filter((value)=>{ 
      return value==='P' //배열 내의 대문자 P인  요소들을 반환.
  })
  var y = split.filter((value)=>{
      return value==='Y' //배열 내의 대문자 Y인  요소들을 반환.
  })
  var plength = p.length 
  var ylength = y.length
  //p와 y 배열의 길이(개수) 구하기

  if(plength==ylength){
      return true //길이(개수)가 같다면 true 반환
  }else{
      return false //그 외(개수가 다르다면) false 반환
  }
}
~~~

### 17. 문자열 다루기 기본

~~~
문제 설명
문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요. 예를 들어 s가 "a234"이면 False를 리턴하고 "1234"라면 True를 리턴하면 됩니다.

제한 사항
s는 길이 1 이상, 길이 8 이하인 문자열입니다.
s는 영문 알파벳 대소문자 또는 0부터 9까지 숫자로 이루어져 있습니다.
~~~
사용한 메서드:
[parseInt()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
```js
function solution(s) {
    
  let result = parseInt(s) //s를 정수로 변환 -> 문자열이 껴있으면 NaN이 출력

  return (s.length === 4 || s.length === 6) && s==result ? true : false
}
```

### 18. 서울에서 김서방 찾기

```
문제 설명
String형 배열 seoul의 element중 "Kim"의 위치 x를 찾아, "김서방은 x에 있다"는 String을 반환하는 함수, solution을 완성하세요. seoul에 "Kim"은 오직 한 번만 나타나며 잘못된 값이 입력되는 경우는 없습니다.

제한 사항
seoul은 길이 1 이상, 1000 이하인 배열입니다.
seoul의 원소는 길이 1 이상, 20 이하인 문자열입니다.
"Kim"은 반드시 seoul 안에 포함되어 있습니다.
```

```js
function solution(seoul) {
  for(let i=0; i<seoul.length;i++){
      if(seoul[i]=='Kim'){
          return `김서방은 ${i}에 있다`
      }
  }
}
```

### 19. 수박수박수박수박수박수?

```
문제 설명

길이가 n이고, "수박수박수박수...."와 같은 패턴을 유지하는 문자열을 리턴하는 함수, solution을 완성하세요. 예를들어 n이 4이면 "수박수박"을 리턴하고 3이라면 "수박수"를 리턴하면 됩니다.
제한 조건
n은 길이 10,000이하인 자연수입니다.
```

```js
function solution(n) {
  var answer = '';
  let watermelon = ['수','박']
  for(let i=1; i<=n; i++){
      if(i%2==1){
      answer+=watermelon[0]//i가 홀수라면 answer에 '수'를 더해줌
      }else{
      answer+=watermelon[1]//i가 짝수라면 answer에 '박'을 더해줌
      }
  }
  console.log(answer)
  return answer;
}
```

### 20. 완주하지 못한 선수

```
문제 설명
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.
마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

제한사항
마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
completion의 길이는 participant의 길이보다 1 작습니다.
참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
참가자 중에는 동명이인이 있을 수 있습니다.
```
사용한 메서드: 
[sort()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
```js
function solution(participant, completion) {
    participant.sort()
    completion.sort()
    for(let i = 0; i<participant.length; i++){
        if(participant[i] !== completion[i])
            return participant[i]
    }
}

```
