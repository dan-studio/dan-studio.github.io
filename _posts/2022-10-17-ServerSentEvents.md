---
layout: single 

title:  "SSE(Server Sent Events)"  
categories: React
createDate: "2022-10-17"
tags: react
toc: true
header:
sidebar: 
---



파이널 프로젝트를 하면서 실시간 알림기능을 구현하려고 웹소켓에 대하여 알아보던 중 지속적인 연결이 필요한 웹소켓과는 달리 http 연결만 되어 있으면 클라이언트 요청 없이도 서버에서 클라이언트로 데이터를 보낼 수 있는 SSE(Server Sent Event) 라는 방법이 더 효율적일것이라는 생각이 들어 SSE에 대해 알아보았다.

**웹소켓과 SSE(Server-Sent-Event)에 차이점**

WebSocket과 SSE에 차이점은 WebSocket은 양방향으로 데이터를 주고 받을 수 있지만 SSE(Server-Sent-Event)를 사용하게 되면 클라이언트는 데이터를 받을 수만 있게 단방향으로 데이터를 주고받는다.

**Server-Sent Events 사용하기**

Server-Sent Event API는 [EventSource ](https://developer.mozilla.org/en-US/docs/Web/API/EventSource)인터페이스에 포함돼 있다. 이벤트를 전달 받기 위해서 서버로 접속을 시작하려면 우선, 이벤트를 생성하는 서버측 스크립트를 URI로 지정하여 새로운 [EventSource](https://developer.mozilla.org/en-US/docs/Web/API/EventSource) 객체를 생성한다.

```js
const eventSource = new EventSource("url here")
```

이벤트 소스를 생성 했다면 `message` 이벤트에 대한 핸들러를 등록하여 서버로부터의 메시지 수신을 시작할 수 있다.

```js
eventSource.onmessage = (e) => { //이벤트를 수신
  
}

eventSource.close() // sse 메시지 수신 중지
```

문제가 발생한 경우에는 오류 이벤트를 생성한다. `EventSource` 갹채에 `onerror` 콜백을 등록하면 에러를 프로그램으로 대처할 수 있다.

```js
evtSource.onerror = function(e) {
  alert("EventSource failed.");
};
```



출처: https://developer.mozilla.org/ko/docs/Web/API/Server-sent_events/Using_server-sent_events
