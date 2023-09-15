# Q4. What will be the output-02?

## ❓ Question

```js
const btn = document.getElementById("btn");

btn.addEventListener(
  "click",
  (event) => {
    event.stopPropagation();
    console.log("handler1");
  },
  true
);

btn.addEventListener(
  "click",
  (event) => {
    event.stopPropagation();
    console.log("handler2");
  },
  true
);

btn.addEventListener("click", (event) => {
  event.stopPropagation();
  console.log("handler3");
});
```

<br />

- [x] handler1, handler2, handler3
- [ ] handler1, handler2
- [ ] handler1
- [ ] handler3, handler1, handler2
- [ ] handler3

## 🤔 My Thinking

`stopPropagation`을 실행하면 캡쳐링/버블링을 포함한 이벤트 전파를 막는다. <br />
캡쳐링과 버블링은 실제 이벤트가 발생한 DOM 엘리먼트로 이벤트 실행 순서(turn)가 넘어가지 전/후 단계에서 해당 이벤트를 사전/사후에 감지할 수 있는 시스템이기 때문에
이벤트가 발생한 실제 DOM 엘리먼트에서는 캡쳐링이나 버블링에 대한 설정 값은 무효하다. <br />
그러므로 실제 이벤트가 발생한 target이 btn일 경우, 핸들러가 등록된 순서대로 모두 실행이 되며 이벤트 전파 단계일 경우엔 handler1, handler2가 먼저 캡쳐링 단계에서 실행이 되고 이후 버블링 단계에서 handler3이 실행이 된다.

## 🤓 Answer

Explanation.

addEventListener(type, listener, useCapture)

All events begin at the window and first go through the capturing phase.
This means that when an event is dispatched, it starts the window and travels "downwards" towards its target element first.

If you listen for an event with useCapture = true, that's where the corresponding event handler will fire.

Next comes the bubble phase when the event is traveling "up" the DOM tree.
At this point, the event handler with useCapture = false will fire.

So normally our events would fire in the following sequence: handler 1, handler 2, handler 3.

However, the stopPropagation() method is called in our handlers. When you call it, the event will, from that point, cease propagating to any elements it would otherwise travel to.

So if you call stopPropagation() anywhere in the capturing phase, the event will never make it to the target phase or bubbling phase.

Since we called the stopPropagation() in the capture phase and handler 3 is in the bubble phase, it will not be called.

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener

> https://web.dev/eventing-deepdive/
