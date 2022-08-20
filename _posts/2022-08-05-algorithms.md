---
layout: single
title:  "Innovation Camp Algorithm feat.Programmers (day5)"
categories: algorithm
---
[repository](https://github.com/dan-studio/algorithms)
  
미니프로젝트가 끝나고 다음 관문인 알고리즘으로 넘어오게 되었다.
[프로그래머스](https://school.programmers.co.kr)의   난이도가 가장 낮은 문제부터 해결을 해나갔으나 너무나도 생소한 분야이기 때문에   처음부터 어려움을 많이 겪게 되었다.  
(문제의 번호는 이번 innovation camp에서 할당한 번호 기준)


### 1. 직사각형 별찍기
~~~
이 문제에는 표준 입력으로 두 개의 정수 n과 m이 주어집니다.
별(*) 문자를 이용해 가로의 길이가 n, 세로의 길이가 m인 
직사각형 형태를 출력해보세요.
~~~
별찍기 문제는 for문을 사용하여 해결하였다.
```js
process.stdin.setEncoding('utf8');
process.stdin.on('data', data => {
    const n = data.split(" ");
    const a = Number(n[0]), b = Number(n[1]);
    for(let i=0; i<b; i++){
            console.log('*'.repeat(a))
}});
```
이 때 주어진 횟수만큼 문자열을 반복해  붙인 새로운 문자열을 반환하는 
[repeat() 메서드](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/repeat)를 사용하였다.


### 2. 짝수와 홀수
~~~
문제 설명
정수 num이 짝수일 경우 "Even"을 반환하고 홀수인 경우 "Odd"를 반환하는 함수, 
solution을 완성해주세요.

제한 조건
num은 int 범위의 정수입니다.
0은 짝수입니다.
~~~
해당 문제는 [삼항 연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)를 사용해 쉽게 해결했다.
~~~js
function solution(num) {
    var answer = '';
    return (num % 2 == 0 ? "Even":"Odd");
}
~~~

### 3. 가운데 글자 가져오기
~~~
문제 설명
단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 
단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.

재한사항
s는 길이가 1 이상, 100이하인 스트링입니다.
~~~
이번 문제를 풀면서 궁금했던 부분은 길이가 홀수인 문자열을 반으로 나눴을 때 ex)'abcde' 문자열은 5자리이며 이를 반으로 나누면 2.5이지만 
따로 주어진 숫자와 같거나 작은 정수 중에서 가장 큰 수를 반환하는 [Math.floor()함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) 없이 'c'를 반환한 것이다.
(나중에 튜터님께 질문드릴 예정)
~~~js
function solution(s) {
  var answer = '';
  var length = s.length     //단어 s의 길이 구하기
  var half = length/2 
  if (length % 2 == 0) {    //길이가 짝수일 때
    answer = s.slice(half-1,half+1);
  } else {  //길이가 홀수일 때
    answer = s.slice(half,half+1);
  }
  return answer;
}
~~~

### 4. 두 정수 사이의 합


~~~
문제 설명
두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, 
solution을 완성하세요. 
예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.

제한 조건
a와 b가 같은 경우는 둘 중 아무 수나 리턴하세요.
a와 b는 -10,000,000 이상 10,000,000 이하인 정수입니다.
a와 b의 대소관계는 정해져있지 않습니다.
~~~
오랜 시간동안 붙잡고 있다가 다른 사람의 풀이를 참고하여 이해하면서 코드를 작성해 보았다.

입력받은 숫자 중 가장 큰 숫자를 반환하는 
[Math.max()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/max) 함수와, 
가장 작은 숫자를 반환하는  
[Math.min()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/min)함수가 도움이 되었다.

for문을 추가해 a와 b 두 숫자 중 작은 숫자로 부터 가장 큰 수까지 1의 단위로 더해 값을 구할 수 있다.
```js
function solution(a, b) {
  var answer = 0;
  var max = Math.max(a,b)
  var min = Math.min(a,b)
  for(let i=min; i<=max;i++){
      answer +=i
  }
  return answer
}
```

### 5. 문자열을 정수로 바꾸기
```
문제 설명
문자열 s를 숫자로 변환한 결과를 반환하는 함수, 
solution을 완성하세요.

제한 조건
s의 길이는 1 이상 5이하입니다.
s의 맨앞에는 부호(+, -)가 올 수 있습니다.
s는 부호와 숫자로만 이루어져있습니다.
s는 "0"으로 시작하지 않습니다.
```
가장 쉬웠다.
[parseInt()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/parseInt) 함수를 사용하면 끝!
```js
function solution(s) { 
    
  return parseInt(s); 
} 
console.log(solution('-1234'))
```
### 6. 없는 숫자 더하기
```
문제 설명

0부터 9까지의 숫자 중 일부가 들어있는 정수 배열 numbers가 매개변수로 주어집니다. 
numbers에서 찾을 수 없는 0부터 9까지의 숫자를 모두 찾아 더한 수를 
return 하도록 solution 함수를 완성해주세요.

제한사항
1 ≤ numbers의 길이 ≤ 9
0 ≤ numbers의 모든 원소 ≤ 9
numbers의 모든 원소는 서로 다릅니다.

입출력 예
numbers	result
[1,2,3,4,6,7,8,0]	14
[5,8,4,0,6,7,9]	6

입출력 예 설명
입출력 예 #1
5, 9가 numbers에 없으므로, 5 + 9 = 14를 return 해야 합니다.

입출력 예 #2
1, 2, 3이 numbers에 없으므로, 1 + 2 + 3 = 6을 return 해야 합니다.
```
이 문제 또한 메서드를 통해 풀수 있다.
여기서 쓰이는 메서드는 [includes()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)를 사용해 for문으로 1부터 9까지의 숫자 중 number배열에 포함되지 않는 수 i를 찾아 모두 더해주도록 하면 된다.
~~~js
function solution(numbers) {
    var answer = 0;
    for(i=0;i<10;i++){
        if(!numbers.includes(i)) answer+=i
    }
    return answer;
}
~~~
### 7. 음양 더하기
~~~
문제 설명
어떤 정수들이 있습니다. 이 정수들의 절댓값을 차례대로 담은 정수 배열 
absolutes와 이 정수들의 부호를 차례대로 담은 불리언 배열 
signs가 매개변수로 주어집니다. 
실제 정수들의 합을 구하여 return 하도록 solution 함수를 완성해주세요.

제한사항
absolutes의 길이는 1 이상 1,000 이하입니다.
absolutes의 모든 수는 각각 1 이상 1,000 이하입니다.
signs의 길이는 absolutes의 길이와 같습니다.
signs[i] 가 참이면 absolutes[i] 의 실제 정수가 양수임을, 
그렇지 않으면 음수임을 의미합니다.

입출력 예
absolutes	signs	result
[4,7,12]	[true,false,true]	9
[1,2,3]	[false,false,true]	0

입출력 예 설명
입출력 예 #1
signs가 [true,false,true] 이므로, 실제 수들의 값은 각각 4, -7, 12입니다.
따라서 세 수의 합인 9를 return 해야 합니다.

입출력 예 #2
signs가 [false,false,true] 이므로, 실제 수들의 값은 각각 -1, -2, 3입니다.
따라서 세 수의 합인 0을 return 해야 합니다.
~~~
이번 문제는 배열내의 음, 양수들을 합하는 문제이므로 [forEach()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)메서드를 통해 풀어보도록 하자.

forEach() 메서드 안에 if문을 넣어 signs[idx]의 값이 true면 answer에 값을 더해주고 false라면 answer에 값을 빼주는 방식으로 코드를 짰다.
~~~js
function solution(absolutes, signs) {
    var answer = 0;
 absolutes.forEach((val, idx)=>{
     if(signs[idx]){
         answer+=val
     }else{
         answer-=val
     }
 })
    return answer;
}
~~~

### 8. 평균 구하기
```
문제 설명

정수를 담고 있는 배열 arr의 평균값을 return하는 함수, solution을 완성해보세요.

제한사항
arr은 길이 1 이상, 100 이하인 배열입니다.
arr의 원소는 -10,000 이상 10,000 이하인 정수입니다.

```
앞서 해결한 문제들의 경험을 살려 이번 문제에도 배열이 나왔기 때문에 [forEach()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) 메서드를 사용하여 풀게 되었다.
모든 요소들을 더해준 후 [array.length](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/length)로 나누어서 평균을 쉽게 구할 수 있다.
```js
function solution(arr) {
  var answer = 0;
  arr.forEach((i)=>{
      answer+=i
  })
  return answer/arr.length;
}
```
### 9. 핸드폰 번호 가리기

```
문제 설명

프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 
고객들의 전화번호의 일부를 가립니다.
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 
나머지 숫자를 전부 *으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.

제한 조건
phone_number는 길이 4 이상, 20이하인 문자열입니다.
```
이번 문제는 문자열인 번호의 끝 4자리를 제외한 모든 문자를 '*'
로 변환해야 하기 때문에 [slice()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/slice)메서드를 사용하게 되었다.

끝 4자리를 기준으로 앞에있는 숫자와 나눈다음 앞의 숫자의 길이만큼
1번 문제에서 나왔던 [repeat()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/repeat)메서드를 사용해 별모양으로 변환을 하여 문제를 해결하였다.

```js
function solution(phone_number) {
    let back = phone_number.slice(-4)
    let front = phone_number.slice(0, -4)
    let length = front.length
     
    var star = '*'
    var stars = star.repeat(length)
    
    
    var phone_number = stars+back;
    return phone_number;
}
console.log(solution('01000001111'))
```
