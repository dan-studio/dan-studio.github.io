---
layout: single
title:  "[Redux] Ducks Pattern (day24)" 
subtitle: "What Is DUCKS Pattern?"
createDate: "2022-08-24"
categories: Redux
tags: redux
header:
  teaser: "/assets/images/Redux.jpeg"
---

![img](https://velog.velcdn.com/images/danchoi/post/b3f6674f-6f68-4b61-98fd-527cc88648f1/image.jpeg)

# 덕스 패턴(ducks pattern)이란?

- 액션 타입(Action types), 액션 생성 함수(Action Creators), 리듀서(Reducer)를 각각의 별도의 파일이 아닌 한 파일 안에 작성한다.
- 자바스크립트 개발자인 Erik Rasmussen이 리덕스 사용 방법과 관련하여 제안한 패턴이다.
- 덕스 패턴을 이용하여 리덕스를 모듈화하는 것의 이점은 코드를 작성하는 사람도 왔다갔다 하지 않고 하나의 파일 안에서 *액션 타입 => 액션 생성 함수 => 리듀서* 이런 식으로 순서대로 작성하기만 하면 되기 때문에 코드 작성하기가 더 용이하고, 다른 사람들이 보기에도 코드가 깔끔 명료하고 가독성이 좋다는 것이다.

# Ducks pattern의 규칙

- MUST **export default** a function called **reducer()**
  반드시 리듀서 함수를 default export 해야한다.
- MUST **export** its action creators as functions
  반드시 액션 생성 함수를 export 해야한다.
- MUST have action types in the form **npm-module-or-app/reducer/ACTION_TYPE**
  반드시 접두사를 붙인 형태로 액션 타입을 정의해야 한다. (아래 예제 코드 참고)
- MAY **export** its action types as **UPPER_SNAKE_CASE**, if an external **reducer** needs to listen for them, or if it is a published reusable library
  (필수는 아니지만) 외부 리듀서가 모듈 내 액션 타입을 바라보고 있거나, 모듈이 재사용 가능한 라이브러리로 쓰이는 것이라면 액션 타입을 UPPER_SNAKE_CASE 형태로 이름 짓고 export 하면 된다.

```js
//initialState
const initialState = {
  todo:[
    {
      id: 1,
      title: "go  to the gym",
      body: "from 9am",
      isDone: false,
    },
  ]
}

// Actions
const CREATE = 'todo/CREATE';
const READ = 'todo/READ';
const UPDATE = 'todo/UPDATE';
const DELETE   = 'todo/DELETE';

// Action Creators
export function create_todo(todo) {
  return { type: CREATE, todo };
}

export function read_todo(id) {
  return { type: READ, id };
}

export function update_todo(id) {
  return { type: UPDATE, id };
}

export function delete_todo(id) {
  return { type: DELETE, id };
}

// Reducer
export default function reducer(state = initialState, action = {}) {
  switch (action.type) {
    case CREATE: {
          const new_todo_list = [...state.list, action.todo];
          return { ...state, list: new_todo_list };
      }
      .
      .
      .
      
    default: return state;
  }
}
```

