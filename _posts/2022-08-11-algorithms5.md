---

layout: single
title:  "Innovation Camp Algorithm feat.Programmers (day11)"
categories: algorithm
tags: algorithm
toc: true
sidebar: 
    nav: "docs"
---

[repository](https://github.com/dan-studio/algorithms)



지루할줄만 알았던 이노베이션 캠프 2주차 알고리즘 주의 마지막날. 
처음에는 푸는 방법조차 몰랐기 때문에 어려움을 겪었으나
일주일이 지난 지금은 스스로 문제를 분석하고 접근할 수 있다는 점이 상당히 뿌듯했다.
시험을 마치고 몇문제를 더 풀어보았다.

### 21. 이상한 문자 만들기

```
문제 설명
문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 
각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 
각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 
바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

제한 사항
문자열 전체의 짝/홀수 인덱스가 아니라, 
단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.

입출력 예
s					return
"try hello world"	"TrY HeLlO WoRlD"
```
사용한 메서드
[split()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/split)
[toUpperCase()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase)
[toLowerCase()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)
[push()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
[join()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

```js
function solution(s) {
  var answer = []
  var words = s.split(' ') //단어별로 나누어 배열에 담아줍니다.
  for(let i=0; i<words.length; i++){
      var word = words[i] //배열 내의 단어
      var result = []
      for(let j=0; j<word.length; j++){ 
          if(j%2==0){	//단어의 글자중 짝수라면 대문자로 변환
              result += word[j].toUpperCase()
          }else{//그 외(홀수)라면 소문자로 변환
              result += word[j].toLowerCase()
          }
      }
      answer.push(result)// 변환된 결과를 answer 배열에 담아주고
  }
  return answer.join(' ') //answer 배열의 요소들 사이 ' '를 붙여 문자열로 변환해준다.
}
```

### 22. 자릿수 더하기

```
문제 설명
자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요.
예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.

제한사항
N의 범위 : 100,000,000 이하의 자연수

입출력		예
N		answer
123		6
987		24

```
사용한 메서드:
[split()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/split)
[map()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
사용한 생성자:
[String()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String#문자열_변환)
[Number()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number/Number)
```js
function solution(n){
  var answer = 0;
  var split = String(n).split('')//숫자열 n을 문자열로 변경 후 각 숫자를 배열에 넣는다.
  var num = split.map((x)=>Number(x))//배열에 들어간 요소들을 숫자열로 변경한다.
  for(let i=0;i<num.length;i++){
      answer += num[i] //answer에 배열내 모든 요소들을 더해준다
  }
  return answer
}
```

### 23. 자연수 뒤집어 배열로 만들기

```
문제 설명
자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 
예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.

제한 조건
n은 10,000,000,000이하인 자연수입니다.

입출력 예
n		return
12345	[5,4,3,2,1]
```
사용한 메서드:
[split()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/split)
[reverse()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)
[map()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
사용한 생성자:
[Number()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number/Number)
```js
function solution(n) {
  return reverse=String(n).split('').reverse().map(x=>Number(x))
  }
```

### 24. 정수 내림차순으로 배치하기

```
문제 설명
함수 solution은 정수 n을 매개변수로 입력받습니다. 
n의 각 자릿수를 큰것부터 작은 순으로 정렬한 새로운 정수를 리턴해주세요. 
예를들어 n이 118372면 873211을 리턴하면 됩니다.

제한 조건
n은 1이상 8000000000 이하인 자연수입니다.

입출력 예
n		return
118372	873211
```
사용한 메서드:
[split()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/split)
[sort()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
사용한 함수:
[parseInt()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
사용한 생성자:
[String()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String#문자열_변환)
```js
function solution(n) {

  var result = ''
  var answer = String(n).split('')//숫자열 n을 문자열로 변경 후 각 숫자를 배열에 넣는다.
  answer.sort(function(a,b){
      return b-a//내림차순으로 정렬
  })
  for(let i=0; i<answer.length; i++){
      result+=answer[i]//result에 배열내 모든 값을 더해준다
  }
  return parseInt(result);//result를 정수로 반환한다.
}
```

### 25. 정수 제곱근 판별

```
문제 설명
임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하려 합니다.
n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, 
n이 양의 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하세요.

제한 사항
n은 1이상, 50000000000000 이하인 양의 정수입니다.

입출력 예
n	return
121	144
3	-1
```
사용한 메서드:
[isInteger()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number/isInteger)
사용한 함수:
[Math.sqrt()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/sqrt)
```js
function solution(n) {
  var x = Math.sqrt(n)//n의 제곱근을 구한다.
  return Number.isInteger(x)?(x+1)**2:-1//n의 제곱근인 x가 정수라면 ? true : false
}
```
### 26. 제일 작은 수 제거하기

```
문제 설명
정수를 저장한 배열, arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수, 
solution을 완성해주세요. 단, 리턴하려는 배열이 빈 배열인 경우엔 배열에 -1을 채워 리턴하세요. 
예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴 합니다.

제한 조건
arr은 길이 1 이상인 배열입니다.
인덱스 i, j에 대해 i ≠ j이면 arr[i] ≠ arr[j] 입니다.

입출력 예
arr			return
[4,3,2,1]	[4,3,2]
[10]		[-1]
```
사용한 함수:
[Math.min()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math/min)
사용한 메서드:
[filter()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
```js
function solution(arr) {
  const remove = Math.min(...arr)//arr 배열의 가장 작은 수를 찾아준다.
  const filtered = arr.filter((x)=>x!==remove)//arr에서 Math.min()으로 찾은 가장 작은 수를 arr에서 제거해준다.
  return filtered.length<1?[-1]:filtered//길이가 1보다 작다면 ? true : false
  }
```
특이사항: 입출력 예를 보고 착각하여 return의 배열을 내림차 순으로 정렬시켰다.
오늘 실시한 시험에서도 비슷한 착오로 인해 불필요한 코드(?)을 추가해서 단순한 문제 해결에 난항을 겪었다. 
오늘의 교훈: 문제를 잘 읽고 이해한다음 접근하도록 하자