# Q2. What will be the output?

## ❓ Question

```js
const btn = document.getElementById("btn");

btn.addEventListener(
  "click",
  (event) => {
    event.stopImmediatePropagation();
    console.log("handler1");
  },
  true
);

btn.addEventListener(
  "click",
  (event) => {
    event.stopImmediatePropagation();
    console.log("handler2");
  },
  true
);

btn.addEventListener("click", (event) => {
  event.stopImmediatePropagation();
  console.log("handler3");
});
```

<br />

- [ ] handler1, handler2, handler3
- [ ] handler1, handler2
- [x] handler1
- [ ] handler3, handler1, handler2
- [ ] handler3

## 🤔 My Thinking

`stopImmediatePropagation`을 실행하면 해당 이벤트 핸들러를 마지막으로 그 뒤에 실행 예정이었던 이벤트 핸들러는 그 어떤 것도 실행되지 않는다. <br />
같은 이벤트 유형에 대한 다수의 핸들러를 하나의 요소에 부착한 경우, 각각의 핸들러 호출 순서는 부착 순서와 동일하다. <br />
현재 위 코드에선 btn 이라는 엘리먼트를 id 선택자를 통해서 가져왔으며 id는 기본적으로 고유성을 띄고 있기 떄문에 `capture` 옵션이 활성화된 상태로 캡쳐링 단계에서
첫 번째 handler만이 실행된다.

<br>

만약 실제 이벤트의 대상(event target)이 btn 요소가 맞다면, `stopPropagation`을 사용하였다면 handler1과 handler2, handler3 만이 실행되었을 것이다. <br />
stopPropagation은 이벤트의 캡쳐링과 버블링의 전파만 막기 때문에 현재 실행 중인 핸들러 이후의 동작에 대해선 막지 않는다. <br />
캡쳐링과 버블링은 실제 이벤트가 발생한 DOM 엘리먼트로 이벤트 실행 순서(turn)가 넘어가지 전/후 단계에서 해당 이벤트를 사전/사후에 감지할 수 있는 시스템이기 때문에
이벤트가 발생한 실제 DOM 엘리먼트에서는 캡쳐링이나 버블링에 대한 설정 값은 무효하다.

## 🤓 Answer

addEventListener(type, listener, useCapture)

All events begin at the window and first go through the capturing phase. This means that when an event is dispatched, it starts the window and travels "downwards" towards its target element first.

If you listen for an event with useCapture = true, that's where the corresponding event handler will fire.

Next comes the bubble phase when the event is traveling "up" the DOM tree.
At this point, the event handler with useCapture = false will fire.

So normally our events would fire in the following sequence: handler 1, handler 2, handler 3. However, the stopImmediatePropagation() method is called in our handlers.

**It's similar to stopPropagation, but rather than stopping an event from traveling to descendents (capturing) or ancestors (bubbling), this method only applies when you have more than one event handler wired up to a single element. Since addEventListener() supports a multicast style of eventing, it's completely possible to wire up an event handler to a single element more than once. When this happens, (in most browsers), event handlers are executed in the order they were wired up. Calling stopImmediatePropagation() prevents any subsequent handlers from firing.**

## 📄 Reference

> https://medium.com/%EC%98%A4%EB%8A%98%EC%9D%98-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/stoppropagation-vs-stopimmediatepropagation-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-75edaaed7841

> https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener

> https://web.dev/eventing-deepdive/
