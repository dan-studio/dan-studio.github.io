---
layout: single
title:  "Innovation Camp Algorithm feat.Programmers (day8)"
categories: algorithm
---
[repository](https://github.com/dan-studio/algorithms3)



### 13. 2016년

```
문제 설명
2016년 1월 1일은 금요일입니다. 2016년 a월 b일은 무슨 요일일까요? 두 수 a ,b를 입력받아 2016년 a월 b일이 무슨 요일인지 리턴하는 함수, solution을 완성하세요. 요일의 이름은 일요일부터 토요일까지 각각 SUN,MON,TUE,WED,THU,FRI,SAT
입니다. 예를 들어 a=5, b=24라면 5월 24일은 화요일이므로 문자열 "TUE"를 반환하세요.

제한 조건
2016년은 윤년입니다.
2016년 a월 b일은 실제로 있는 날입니다. (13월 26일이나 2월 45일같은 날짜는 주어지지 않습니다)
```

```js
function solution(a, b) {
  var week = ['SUN','MON','TUE','WED','THU','FRI','SAT']//요일은 0부터 반환하기 때문에 예를들어 입력한 날짜가 화요일이면 2를 return 한다. 그러므로 일요일부터 배열에 담았다.
  var getDay = week[new Date(2016, a-1, b).getDay()]//month도 0(1월)부터 시작한다 따라서 -1을 했다.
  
  return getDay;
}
```

엄청 어려운 문제일줄 알았으나 [Date()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/Date)생성자를 활용해 문제를 해결하니 별것 아니였다.
날짜, 요일관련 문제가 나온다면 Date()를 항상 이용하도록 해야겠다!

### 14.나누어 떨어지는 숫자 배열


~~~
문제 설명
array의 각 element 중 divisor로 나누어 떨어지는 값을 
오름차순으로 정렬한 배열을 반환하는 함수, solution을 작성해주세요.
divisor로 나누어 떨어지는 element가 하나도 없다면 배열에 
-1을 담아 반환하세요.

제한사항
arr은 자연수를 담은 배열입니다.
정수 i, j에 대해 i ≠ j 이면 arr[i] ≠ arr[j] 입니다.
divisor는 자연수입니다.
array는 길이 1 이상인 배열입니다.
~~~
~~~js
function solution(arr, divisor) {
  var answer = [];
  
  for(let i = 0; i<arr.length; i++){
  if(arr[i]%divisor==0){
      answer.push(arr[i])
  }
  }
  if(answer.length==0){
      answer.push(-1)//나누어 떨어지는 값이 없으면 -1 반환
  }
  answer.sort(function(a, b)  {
return a - b;
});//오름차 순으로 정렬해줌. 내림차 순은 b-a
  console.log(answer)
  return answer;
}
~~~
~~~
15. 내적
문제 설명
길이가 같은 두 1차원 정수 배열 a, b가 매개변수로 주어집니다. a와 b의 내적을 return 하도록 solution 함수를 완성해주세요.
이때, a와 b의 내적은 a[0]*b[0] + a[1]*b[1] + ... + a[n-1]*b[n-1] 입니다. (n은 a, b의 길이)

제한사항
a, b의 길이는 1 이상 1,000 이하입니다.
a, b의 모든 수는 -1,000 이상 1,000 이하입니다.

입출력 예
a			b			result
[1,2,3,4]	[-3,-1,0,2]	 3
[-1,0,1]	[1,0,-1]	-2
~~~

~~~js
function solution(a, b) {
  var answer = 0;
  for(let i=0;i<a.length;i++){
      const arr=a.map(x=>a[i]*b[i])//a,b배열의 i번째를 전부 더해주고
                  answer+=arr[i]//answer의 값에 배열 내 모든 값을 더해준다
  }
  return answer;
}
~~~
[map()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)메서드를 사용했다. 잘쓴게 맞나 싶지만.. 일단 정답은 잘 나온다.
