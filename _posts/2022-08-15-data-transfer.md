--- 
layout: single 
title:  "[React] 컴포넌트 간의 데이터 전달 방법  (day15)" 
categories: React
tags: react
---

![post-thumbnail](https://velog.velcdn.com/images/danchoi/post/bad31f41-5e76-4ab0-b60e-cb4742e30d19/image.jpeg)

![](https://3ulsmb4eg8vz37c0vz2si64j-wpengine.netdna-ssl.com/wp-content/uploads/2019/05/react-native-UX-design.gif)

> 1. 부모에서 자식으로 전달
> -> props를 이용한다.



App.jsx
```jsx
import React, { useState } from "react";
import Child from "./Child";

function App() {
  const [data, setData] = useState("helloWorld");

  return <Child data={data}></Child>;
}

export default App;
```

Child.jsx
```jsx
import React from "react";

function Child({ data }) {
  console.log(data);
  return <div>Child</div>;
}

export default Child;
```
Result
```console
helloWorld										Child.jsx:4 helloWorld
```

> 2. 자식에서 부모로 전달
> -> 함수를 이용한다.

자식은 props를 사용해서 부모에게 데이터를 건네줄 수 없다.
따라서 부모 컴포넌트에서 함수를 정의하고 이 함수를 자식 컴포넌트에 props로 내려주면, 자식이 데이터를 파라미터로 넣어 호출하는 방식으로 동작한다.

App.jsx

```jsx
import React, { useState } from "react";
import Child from "./Child";

function App() {
  const [data, setData] = useState(0);

  const getData = (data) => {
    setData(data);
  };
  return (
    <div>
      <p>this is parent: {data}</p>
      <Child data={data} getData={getData}></Child>
    </div>
  );
}

export default App;
```

Child.jsx
```jsx
import React from "react";

function Child({ data, getData }) {
  const onClick = () => {
    getData(data + 1);
    console.log(data);
  };
  return (
    <div>
      <button onClick={onClick}>Plus 1</button>
    </div>
  );
}

export default Child;

```
Result
```
0										Child.jsx:6
1										Child.jsx:6
2										Child.jsx:6
3										Child.jsx:6
4										Child.jsx:6
5										Child.jsx:6
6										Child.jsx:6
7										Child.jsx:6
```
![](https://velog.velcdn.com/images/danchoi/post/b91d18d3-4f50-4403-82f1-f92674abda83/image.png)
