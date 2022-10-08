```
layout: single 

title:  "트러블 슈팅"  
categories: React
createDate: "2022-10-08"
tags: react
toc: true
header:
sidebar: 
```

## ⚠️ 에러 내용 및 원인

댓글내의 댓글(대댓글)을 입력하면 첫 대댓글에만 흰화면 및 아래와 같은 오류가 발생하였다.

![스크린샷 2022-10-07 오전 12.34.31](/Users/dan/Desktop/스크린샷 2022-10-07 오전 12.34.31.png)

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