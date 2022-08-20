---
layout: single
title:  "[React] styled-components (day19)" 
subtitle: "styled-components"
createDate: "2022-08-19"
categories: React
tags: react
header:
  teaser: "/assets/images/React.jpeg"
---



# styled-components

```
기존 돔을 만드는 방식인 css, scss 파일을 밖에 두고, 태그나 id, class이름으로 가져와 쓰지 않고, 동일한 컴포넌트에서 컴포넌트 이름을 쓰듯 스타일을 지정하는 것을 styled-components라고 부른다. 
css 파일을 밖에 두지 않고, 컴포넌트 내부에 넣기 때문에, css가 전역으로 중첩되지 않도록 만들어주는 장점이 있다.
```

## how to Install

```
npm install styled-components
```

## example

```jsx
import React from "react";
import styled from "styled-components";
const Todo = ({ todo, remove, onToggle }) => {
  const { id, title, body } = todo;
  return (
    <Container>
      {todo.isDone === false ? (
        <Todos background="rgba(18, 183, 248, 0.13)">
          <Todotitle>{title}</Todotitle>
          <Todobody>{body}</Todobody>
          <Buttons>
            <Todobutton onClick={() => onToggle(id)}>Nailed it! ✅</Todobutton>
            <Todobutton onClick={() => remove(id)}>remove ❌</Todobutton>
          </Buttons>
        </Todos>
      ) : (
        <Todos background="rgba(248, 102, 18, 0.13);">
          <Todotitle>{title}</Todotitle>
          <Todobody>{body}</Todobody>
          <Buttons>
            <Todobutton onClick={() => onToggle(id)}>Cancel ⛔️</Todobutton>
            <Todobutton onClick={() => remove(id)}>remove ❌</Todobutton>
          </Buttons>
        </Todos>
      )}
    </Container>
  );
};
const Container = styled.div`
  margin: auto;
`;
const Todos = styled.div`
  height: 200px;
  width: 300px;
  background-color: ${(props)=>props.background};
  border-radius: 15px;
  position: relative;
`;
```

함수의 인자에서 props를 받아오고, props안에는 부모 컴포넌트에서 보낸 background-color를 return 한다. 

${(props)⇒{ return props.borderColor }} 이렇게 리턴하면 (props)⇒{ return props.borderColor } 의 값이 설정한 Todos background='rgba(18, 183, 248, 0.13)'  가 되고  

브라우저는 background-color: rgba(18, 183, 248, 0.13) 라는 코드로 인식하여 스타일링이 된다.