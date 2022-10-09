---
layout: single 

title:  "트러블 슈팅 (FormData에 관하여...)"  
categories: React
createDate: "2022-10-09"
tags: react
toc: true
header:
sidebar: 
---

# 1

## ⚠️ 에러 내용 및 원인

### form데이터에 담긴 데이터 조회 실패

### formdata를 console에 찍었을때 form데이터에 담긴 데이터 대신 빈객체만 찍혔던 경우

> 원인 :  FormData는 XMLHttpRequest를 사용해 전송할 key/value와 같이 쌍을 이뤄 컴파일한 "특수한 객체"이기 때문에, 문자열로 표현할 수 없어서 빈 객체가 나올수 밖에 없다.

## 🔆 해결 방안

해결책 :

1. "for ...of " 반복문
2. form데이터 내부의 데이터를 확인하는 메소드인 formdata.entries

2가지 방법을 통하여 내부 데이터 확인

```jsx
const addClickHandler = () => {
    let formData = new FormData();
    formData.append(
      "data",
      new Blob([JSON.stringify(addCertify)], { type: "application/json" })
    );
    formData.append("file", image);
		
		////////////////////////////////////
			
1. "for ...of " 반복문
2. form데이터 내부의 데이터를 확인하는 메소드인 formdata.entries

	2가지 사용

    for (let i of formData.entries()) {
      console.log("i", i[1]);
      console.log("formdata", formData);
    }

		////////////////////////////////////
```



# 2

## ⚠️ 에러 내용 및 원인

## formdata로 데이터 전송에 실패했던 경우

원인 : “data”가 key 라는 사실을 몰랐다.

(`formData.append('userpic' //key 설정하는 부분 // ,myFileInput.files[0]'//전달데이터 // );`)

당연히 데이터를 전송하는 것이니 data라고 쓰는줄로 착각함

잘못된 코드

-data라는 키에 addCertify라는 객체를 담아 보냈다.

-각각의 키(title,image)에 맞게 데이터를 따로 담아 보냈어야함

```jsx
const addCertify = {
    title: challengeTitle,
    image: image,

  };
const addClickHandler = () => {
    let formData = new FormData();
    formData.append(
      "data", // key 이름을 설정해주는 부분
      new Blob([JSON.stringify(addCertify)], 
// data라는 키에 2가지 정보를 따로 보내지 않고 
// addCertify라는 객체에 한번에 몰아서 보냈던 것이 문제
{ type: "application/json" })
    );
```

## 🔆 해결 방안

각각의 키(title,image)에 맞게 데이터를 따로 담아 보냄

```jsx
 formData.append(
      "title", // key 이름을 api 명세서대로 설정
      new Blob([JSON.stringify(challengeTitle)], 
// 데이터를 객체에 한번에 담지 않고 나눠서 전달
 { type: "application/json" })
```