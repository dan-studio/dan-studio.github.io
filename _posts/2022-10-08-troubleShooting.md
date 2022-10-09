---
layout: single 

title:  "트러블 슈팅 (null과 배열)"  
categories: React
createDate: "2022-10-08"
tags: react
toc: true
header:
sidebar: 
---



## ⚠️ 에러 내용 및 원인

댓글내의 댓글(대댓글)을 입력하면 첫 대댓글에만 흰화면 및 아래와 같은 오류가 발생하였다.

![](https://velog.velcdn.com/images/danchoi/post/e1ed676c-5654-4f71-8028-9b507ea27794/image.png)

## 기존 코드

```jsx
userApis
      .writeComment(commentMsg)
      .then((res) => {
        console.log(res);
        setCertifyDetail((prev) => {
          return {
            ...prev,
            commentList: [...prev.commentList, res.data],
          };
        });
        setComment("");
      })
      .catch((err) => {
        console.log(err);
      });
```

원인을 찾아보니 댓글 데이터에 대댓글이 null값으로 들어갔기 때문에 해당 오류가 생긴것으로 보였다.

## 🔆 해결 방안

- 방법 1.

  댓글 등록시 spread문법을 이용하여 대댓글에 null이 아닌 빈배열을 넣어준다.

  ```jsx
  userApis
        .writeComment(commentMsg)
        .then((res) => {
          console.log(res);
          setCertifyDetail((prev) => {
            return {
              ...prev,
              commentList: [...prev.commentList, {...res.data, subCommentList:[]}],
            };
          });
          setComment("");
        })
        .catch((err) => {
          console.log(err);
        });
  ```

- 방법 2.

  백엔드에 댓글을 등록할 시 subCommentList(대댓글 리스트)에 null값이 아닌 빈배열([])을 넣어달라고 요청을 한다.

# 결과 

![](https://velog.velcdn.com/images/danchoi/post/b9481833-dfe5-4cc5-9226-bccd50ec3ad7/image.png)