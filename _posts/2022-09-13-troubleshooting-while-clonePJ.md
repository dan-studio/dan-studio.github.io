---
layout: single 

title:  "클론코딩 중 겪은 문제(useEffect)"  
categories: React
createDate: "2022-09-13"
tags: react
toc: true
header:
sidebar: 
---

# 사건의 발단

벨로그 클론코딩을 하던 중 게시글 작성에서 태그입력 기능을 구현하던 중 입력된 마지막 값이 배열에 들어가지 않는 문제를 발견하게 된다.

부모컴포넌트로 부터 useState를 통해 자식 컴포넌트(tag Input)에 입력된 값(array)를 전달받아야 하는데 배열의 마지막 값을 가져오지 못하는것이 내 발목을 붙잡았다.



# 해결 과정

<img src="https://velog.velcdn.com/images/danchoi/post/85fffb0c-36f2-41a3-8414-db8b7914b4e3/image.png" alt="img" style="zoom:50%;" />

(tag Input에 입력된 마지막 값이 console에는 찍히지 않음)

하지만 자식컴포넌트 자체에서 콘솔에 찍었을 때는 입력된 모든 값이 잘 나오는 점을 확인하였다.

<img src="https://velog.velcdn.com/images/danchoi/post/59b3c145-25d1-4247-baec-1bbf7099b7cd/image.png" alt="img" style="zoom:50%;" />

따라서 부모 컴포넌트로 부터 넘어온 props를 useEffect 안에 넣어줬다.

```js
const Parent = () => {
const [tag, setTag] = useState([]);
return (
	<>
		<Child setTag={setTag}/>
	</>
)
}


const Child = ({setTag}) => {
const [tagList, setTagList] = useState([])
useEffect(()=>{
	setTag(tagList)
})
}

```

이 때 컴포넌트가 렌더링될 때마다 useEffect가 호출되도록 의존성 배열을 제거해줬다.

그렇게 태그를 추가하니 정상적으로 부모 컴포넌트에 배열의 모든 데이터들이 정상적으로 넘어가는것을 확인할 수 있었다.

# useEffect

다시 한번 useEffect를 짚고 넘어가자면

<img src="https://velog.velcdn.com/images/danchoi/post/87eadc86-f5f4-436a-9cf2-55b332c4dee6/image.png" alt="img" style="zoom:50%;" />

![img](https://velog.velcdn.com/images/danchoi/post/9a37790f-a379-4a24-87fc-0c5facdcb392/image.png)

1. useEffect(callback)

```js
useEffect(()=>{
  // Runs after Every Rendering
})
```

2. useEffect(callback,[])

```js
useEffect(()=>{
  // Runs ONCE after initial rendering
}, [])
```



3. useEffect(callback, [prop, state])

```js
useEffect(()=>{
  // Runs ONCE after initial rendering
  // and after every rendering ONLY IF 'prop' or 'state' changes
}, [prop, state])
```

