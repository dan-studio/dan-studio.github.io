---
layout: single 

title:  "storages"  
categories: web
createDate: "2022-09-27"
tags: react
toc: true
header:
sidebar: 
---

# Axios Intercepter란?

> interceptor는 .then() 이나 .catch()로 처리되기 전 요청이나 응답을 가로챌 수 있다.
>
> 요청을 보낼 때 토큰을 붙이거나, 응답을 받아서 처리하기 전 가로채서 오류 처리를 먼저하고 싶을 때 등 다양하게 활용이 가능하다.

## how to use?

1. axios 객체 생성

   ```js
   import axios from "axios";
   
   const instance = axios.create({
     headers: {"Content-Type": "application/json"}
   });
   
   export default instance
   ```

2. axios 객체.interceptors.request.use(); 

   ```js
   //request
   instance.interceptors.request.use(config => {
   	config.headers["TOKEN_KEY"] = "TOKEN_VALUE"
     //config.headers.common.TOKEN_KEY="TOKEN_VALUE"
     return config //return 필수!!
   }, err => {
     return Promise.reject(err)
   })
   
   //response
   instance.interceptors.response.use(config=>{
     return config
   },
   err=>{
     console.log(err)
     return Promise.reject(err)
   })
   ```

   