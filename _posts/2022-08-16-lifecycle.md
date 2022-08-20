--- 
layout: single 

title:  "[React] Component's Lifecycle (day16)" 
categories: React
tags: react
toc: true
header:
  teaser: /assets/images/React.jpeg
sidebar: 
    nav: "main"
---

![post-thumbnail](https://velog.velcdn.com/images/danchoi/post/ad401ad2-d404-4284-9f51-c1ba0239207a/image.jpeg)

## 컴포넌트의 라이프 사이클
은(컴포넌트의 생명주기) 컴포넌트가 렌더링을 준비하는 순간부터, 페이지에서 사라질 때까지를 뜻한다.
(웹페이지 상의 요소가 우리 눈에 보이게 되는 순간부터 닫았을 때 사라지는 순간까지를 라이프사이클이라고 한다.)
![](https://velog.velcdn.com/images/danchoi/post/6c10c549-702f-4763-be73-8cfd3a0a07fa/image.png)

- 컴포넌트는 생성되고 -> 수정(업데이트)되고 -> 사라진다(삭제).
- 생성은 처음으로 컴포넌트를 불러오는 단계이다.
- 수정(업데이트)는 사용자의 행동(클릭, 데이터 입력 등)으로 데이터가 바뀌거나, 부모 컴포넌트가 렌더링할 때 업데이트 된다.
  - props가 바뀔 때
  - state가 바뀔 때
  - 부모 컴포넌트가 업데이트 되었을 때(=리렌더링 했을 때)
  - 또는, 강제로 업데이트 했을 경우(forceUpdate()를 통해 강제로 컴포넌트를 업데이트할 수 있습니다.)
- 제거는 페이지를 이동하거나, 사용자의 행동(삭제 버튼 클릭 등)으로 인해 컴포넌트가 화면에서 사라지는 단계이다.
   - constructor()
   생성자 함수라고도 부른다. 컴포넌트가 생성되면 가장 처음 호출됨.
   - render()
   컴포넌트 의 모양을 정의하는 함수.
   state, props에 접근해서 데이터를 보여줄 수 있음.
   - componentDidMount()
   컴포넌트가 화면에 나타나는 것을 Mount한다고 표현함. 그러므로 didMount() = 마운트가 완료된 상황.
   이 함수는 첫번째 렌더링을 마친 후 딱 한 번 실행됨.(컴포넌트가 리렌더링할 때는 실항안됨.)
  보통은 이 안에서 ajax요청, 이벤트 등록, 함수 호출 등 작업을 처리함. 또, 가상돔이 실제돔으로 올라간 후이기 때문에 DOM관련 처리를 해도 된다.
  - componentDidUpdate(prevProps, prevState, snapshot)
  DidMount()가 첫 렌더링 후에 호출되는 함수라면, DidUpdate()는 리렌더링을 완료한 후 실행되는 함수.
	이 함수에 중요한 파라미터 2개는 prevProps와 prevState이다. 이는 각각 업데이트 되기 전 props, state. 이전 데이터와 비교할 일이 있다면 가져다 쓰도록 한다. DidUpdate()가 실행될 때도 가상돔이 실제돔으로 올라간 후이기 때문에 DOM관련 처리 해도 됨.
   - componentWillUnmount()
   컴포넌트가 DOM에서 제거될 때 실행하는 함수.
    만약 우리가 스크롤 위치를 추적 중이거나, 어떤 이벤트 리스너를 등록했다면 여기에서 해제를 해줘야한다.(컴포넌트 없이 이벤트만 남겨둘 수 없으니)
