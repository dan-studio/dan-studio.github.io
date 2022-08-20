---
layout: single
title:  "Innovation Camp Algorithm 모의고사 (day9)"
categories: algorithm
---


그동안 갈고닦은 알고리즘의 실력을 테스트하기 위해 모의고사를 실시하였다.
주어진 문제들 중 하나를 선택하여 시험을 실시하면 된다.
(참고로 아직 많이 부족하다.😡)

~~~
1번. 몇시간 했더라?

경식이는 항해에서 한 주 동안 공부 기록을 남길 알고리즘을 만들어보기로 결심했다.
항해의 체크인 페이지에는 몇가지 조건이 있는데 이를 만족하는 알고리즘을 만들어보자.

•체크인과 체크아웃은 항상 정시에 진행한 것으로 가정한다.
•체크아웃을 할 때 익일 시간은 24+a 로 계산한다. 즉 새벽 2시는 24+2 인 26으로 표기한다.
•체크인 페이지는 체크아웃이 새벽 5시 정각이나 새벽 5시를 넘어가면 체크아웃을 깜빡한 것으로 간주한다.
따라서 새벽 5시가 넘어가 체크아웃을 하게 되면 자동으로 체크아웃을 오후 9시(21시)로 한 것으로 처리한다.

제한 조건

•체크인(checkin)과 체크아웃(checkout)을 진행한 시간이 담긴 배열 두 개가 주어진다.
•각 배열에는 월요일부터 일요일까지 체크인/아웃을 한 시간이 담겨있다.
•checkin과 checkout 배열의 길이는 각각 7 이다.

지정입력값
checkIn = [9, 9, 9, 9, 7, 9, 8]
checkOut = [23, 23, 30, 28, 30, 23, 23]
result = 102
~~~
~~~js
const solution = (arr1, arr2) => {
  var result=[]
  var sum=0
  arr1 = [9,9,9,9,7,9,8] // 체크인 시간
  arr2 = [23,23,30,28,30,23,23] // 체크아웃 시간
  for(let i=0;i<arr2.length;i++){ //arr1과 arr2의 길이는 서로 동일하므로 해당 길이(7)만큼 i를 증가시켜준다.
   if(arr2[i]>=29){ //새벽 5시 정각은 24+5인 29이므로 5시가 넘어가면 21시 체크아웃으로 간주하기 때문에
     result[i]=21-arr1[i] //result배열에 21시에서 체크인 시간을 빼준 값을 넣어준다..
   }else{
     result[i] = arr2[i]-arr1[i] // 그 외 시간에는 체크아웃 배열의 i번째 값에서 체크인 배열의 i번째 값을 빼준 결괏값을 result의 i번째 배열에 대입해준다.
   }
    sum+=result[i]//sum의 값에 result의 모든 요소들을 더한다.
  }
  return sum
}
~~~

2번. 신대륙 발견
~~~
예지는 오늘 항해99를 시작했다. 성격이 급한 예지는 항해 1일 차부터 언제 수료를 하게될 지 궁금하다.
항해 1일 차 날짜를 입력하면 98일 이후 항해를 수료하게 되는 날짜를 계산해주는 알고리즘을 만들어보자.
제한 조건
•1 ≤ month ≤ 12
•1 ≤ day ≤ 31 (2월은 28일로 고정합니다, 즉 윤일은 고려하지 않습니다.)

지정입력값
month = 1
day = 18
result = ‘4월 26일’
~~~
이번 문제는 [Date()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/Date) 생성자의 도움을 받아서 해결하였습니다.
~~~js
function solution(month, day) {
  const date = new Date(2022, month - 1, day + 98)//month는 0(1월)부터 11(12월)까지 있기 때문에 -1을 했습니다. 98일 이후 항해를 수료하게 되는 날짜를 구하는 문제이므로 day에는 98일을 더해주었습니다.
  var mm = date.getMonth() + 1 //new Date의 매개변수로 준 month에 1을 뺐기 때문에 다시 1을 더해줍니다.
  var dd = date.getDate()
  return `${mm}월 ${dd}일`;//템플릿 리터럴을 사용해여 변수 mm, dd를 대입합니다.
}
console.log(solution(1, 18))
~~~
