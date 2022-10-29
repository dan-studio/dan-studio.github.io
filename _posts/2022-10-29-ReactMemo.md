---
layout: single 

title:  "React Memo"  
categories: React
createDate: "2022-10-29"
tags: react
toc: true
header:
sidebar: 

---

### `React.memo`

```
const MyComponent = React.memo(function MyComponent(props) {
  /* props를 사용하여 렌더링 */
});
```

100밀리초 미만의 UI응답은 순식간이지만 100에서 300밀리초 사이의 지연은 인지가 가능하다고 한다.

따라서 성능의 향상을 위해, 리엑트는 고차컴포넌트  [고차 컴포넌트(Higher Order Component)](https://ko.reactjs.org/docs/higher-order-components.html) 인 `React.memo`를 지원한다.

React.memo()가 컴포넌트를 감싸면 리액트는 해당 컴포넌트의 렌더된 결과물을 메모리에 기억하므로써 불필요한 렌더링을 건너뛰게 된다.

컴포넌트가 동일한 props로 동일한 결과를 렌더링해낸다면, `React.memo`를 호출하고 결과를 메모이징(Memoizing)하도록 래핑하여 경우에 따라 성능 향상을 누릴 수 있습니다. 즉, React는 컴포넌트를 렌더링하지 않고 마지막으로 렌더링된 결과를 재사용합니다.

`React.memo`는 props 변화에만 영향을 줍니다. `React.memo`로 감싸진 함수 컴포넌트 구현에 [`useState`](https://ko.reactjs.org/docs/hooks-state.html), [`useReducer`](https://ko.reactjs.org/docs/hooks-reference.html#usereducer) 또는 [`useContext`](https://ko.reactjs.org/docs/hooks-reference.html#usecontext) 훅을 사용한다면, 여전히 state나 context가 변할 때 다시 렌더링됩니다.

props가 갖는 복잡한 객체에 대하여 얕은 비교만을 수행하는 것이 기본 동작입니다. 다른 비교 동작을 원한다면, 두 번째 인자로 별도의 비교 함수를 제공하면 됩니다.

```
function MyComponent(props) {
  /* props를 사용하여 렌더링 */
}
function areEqual(prevProps, nextProps) {
  /*
  nextProps가 prevProps와 동일한 값을 가지면 true를 반환하고, 그렇지 않다면 false를 반환
  */
}
export default React.memo(MyComponent, areEqual);
```

# React.memo()를 피해야할 때

```
"컴포넌트가 무겁지 않고 자주 다른 props로 렌더된다면 React.memo()가 그다지 필요하지는 않습니다."
```

이 규칙을 사용해주세요: 성능의 향상을 측정할 수 없다면 메모이제이션을 사용하지 마세요.

```
"잘못 적용된 성능향상 관련 변화들은 오히려 성능에 악영향을 끼칠 수 있습니다. React.memo()를 현명하게 사용하세요."
```

이 메서드는 오직 **[성능 최적화](https://ko.reactjs.org/docs/optimizing-performance.html)**를 위하여 사용됩니다. 렌더링을 “방지”하기 위하여 사용하지 마세요. 버그를 만들 수 있습니다.

출처: https://ko.reactjs.org/docs/react-api.html#reactmemo ,

https://goongoguma.github.io/2021/09/22/Use-React.memo()-wisely/