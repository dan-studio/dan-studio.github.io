---
layout: single 

title:  "useCallback"  
categories: React
createDate: "2022-10-30"
tags: react
toc: true
header:
sidebar: 


---

#### 🚀 **useCallback()**

useCallback은 useMemo와 비슷한 Hook입니다. useMemo는 특정 결괏값을 재사용할 때 사용하는 반면, useCallback은 특정 함수를 새로 만들지 않고 재사용하고 싶을 때 사용하는 함수입니다.

## **useCallback 사용법**

```
const memoizedCallback = useCallback(function, deps);
```

useCallback은 첫 번째 인자로 넘어온 함수를, 두 번째 인자로 넘어온 배열 형태의 함수 실행 조건의 값이 변경될 때까지 저장해놓고 재사용할 수 있게 해 줍니다.

예를 들어 리액트 컴포넌트 안에 함수가 선언되어있을 때 이 함수는 해당 컴포넌트가 렌더링 될 때마다 새로운 함수가 생성되는데, useCallback을 사용하면 해당 컴포넌트가 렌더링 되더라도 그 함수가 의존하는 값(deps)들이 바뀌지 않는 한 기존 함수를 재사용할 수 있습니다.

```
const add = () => x + y;
```

예시로 위와 같은 함수가 있다고 할 때 useCallback을 사용하면 아래와 같이 적용할 수 있습니다.

```
const add = useCallback(() => x + y, [x, y]);
```

출처: https://cocoon1787.tistory.com/798