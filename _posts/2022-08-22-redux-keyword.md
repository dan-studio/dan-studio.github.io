---
layout: single
title:  "[Redux] Keywords for Redux (day22)" 
subtitle: "What Is Redux?"
createDate: "2022-08-22"
categories: Redux
tags: redux
header:
  teaser: "/assets/images/Redux.jpeg"
---

![img](https://velog.velcdn.com/images/danchoi/post/b3f6674f-6f68-4b61-98fd-527cc88648f1/image.jpeg)

# 리덕스에서 사용되는 키워드

### 상태(state)

리덕스에서는 저장하고 있는 상태값("데이터"라고 생각해도 됨)를 state라고 불러요. 딕셔너리 형태({[key]: value})형태로 보관합니다.

### 액션(Action)

상태에 변화가 필요할 때(=가지고 있는 데이터를 변경할 때) 발생하는 것

```javascript
// 액션은 객체예요. 이런 식으로 쓰여요. type은 이름같은 거예요! 저희가 정하는 임의의 문자열을 넣습니다.
{type: 'CHANGE_STATE', data: {...}}
```

액션 객체는 `type` 필드를 필수적으로 가지고 있어야하고 그 외의 값들은 개발자 마음대로 넣어줄 수 있습니다.

```javascript
{
  type: "ADD",
  data: {
    id: 0,
    text: "리덕스 배우기"
  }
}
{
  type: "CHANGE_INPUT",
  text: "안녕하세요"
}
```

### 액션 생성함수 (Action Creator)

액션 생성 함수라고도 부릅니다. 액션을 만들기 위해 사용합니다.

```javascript
//이름 그대로 함수예요!
const addToDo = (text) => {
  // 액션을 리턴합니다! (액션 생성 함수니까요. 제가 너무 당연한 이야기를 했나요? :))
  return {
    type: "ADD",
    text
  };
}

const deleteToDo = (id) => ({ 
  type: "DELETE",
  id
});
```

### 리듀서 (Reducer)

리덕스에 저장된 상태(=데이터)를 변경하는 함수입니다. 우리가 액션 생성 함수를 부르고 → 액션을 만들면 → 리듀서가 현재 상태(=데이터)와 액션 객체를 받아서 → 새로운 데이터를 만들고 → 리턴해줍니다.

```javascript
// 기본 상태값을 임의로 정해줬어요.
const initialState = {
	name: 'mean0'
}

function reducer(state = initialState, action) {
	switch(action.type){

		// action의 타입마다 케이스문을 걸어주면, 
		// 액션에 따라서 새로운 값을 돌려줍니다!
		case CHANGE_STATE: 
			return {name: 'mean1'};

		default: 
			return false;
	}	
}
```



### 스토어 (Store)

우리 프로젝트에 리덕스를 적용하기 위해 만드는 거예요! 스토어에는 리듀서, 현재 애플리케이션 상태, 리덕스에서 값을 가져오고 액션을 호출하기 위한 몇 가지 내장 함수가 포함되어 있습니다. 생김새는 딕셔너리 혹은 json처럼 생겼어요.

내장함수는 공식문서에서 확인할 수 있습니다.

[redux Store](https://ko.redux.js.org/api/store/)

### 디스패치 (dispatch)

디스패치는 스토어의 내장함수 중 하나입니다. 액션을 발생 시키는 역할을 합니다.

 dispatch 라는 함수에는 액션을 파라미터로 전달합니다.

```javascript
// 실제로는 이것보다 코드가 길지만, 
// 간단히 표현하자면 이런 식으로 우리가 발생시키고자 하는 액션을 파라미터로 넘겨서 사용합니다.
dispatch(action); 
```

#### 구독 (subscribe)

구독 또한 스토어의 내장함수 중 하나입니다. subscribe 함수는, 함수 형태의 값을 파라미터로 받아옵니다. subscribe 함수에 특정 함수를 전달해주면, 액션이 디스패치 되었을 때 마다 전달해준 함수가 호출됩니다. 

리액트에서 리덕스를 사용하게 될 때 보통 이 함수를 직접 사용하는 일은 별로 없습니다. 그 대신에 react-redux 라는 라이브러리에서 제공하는 `connect` 함수 또는 `useSelector` Hook 을 사용하여 리덕스 스토어의 상태에 구독합니다.



## 리덕스의 3가지 특징

1. store는 1개만 쓴다
   - 리덕스는 단일 스토어 규칙을 따릅니다. 한 프로젝트에 스토어는 하나만 씁니다.

2. store의 state(데이터)는 오직 action으로만 변경할 수 있다

   - 리액트에서도 state는 setState()나, useState() 훅을 써서만 변경이 가능한데 이는 데이터가 마구잡이로 변하지 않도록 불변성을 유지해주기 위함이다.  

     리덕스에 저장된 데이터 = 상태 = state는 읽기 전용이다. 그런데 액션으로 변경을 일으킨다. → 불변성을 유지하는 데이터를 변경하는 원리는, 가지고 있던 값을 수정하지 않고, 새로운 값을 만들어서 상태를 갈아끼운다는 것이다. 

     즉, A에 +1을 할 때, A = A+1이 되는 게 아니고, A' = A+1이라고 새로운 값을 만들고 A를 A'로 바꾼다.

3. 어떤 요청이 와도 리듀서는 같은 동작을 해야한다

   - 리듀서는 순수한 함수여야 한다는 말이다. 

     순수한 함수라는 건, 

     - 파라미터 외의 값에 의존하지 않아야하고, 
     - 이전 상태는 수정하지(=건드리지) 않는다. (변화를 준 새로운 객체를 return 해야한다.) 
     - 파라미터가 같으면, 항상 같은 값을 반환 
     - 리듀서는 이전 상태와 액션을 파라미터로 받는다.