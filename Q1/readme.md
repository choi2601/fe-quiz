# Q1. When will the loop be pasued?

## ❓ Question

```js
async function foo() {
  for (let i = 0; i < 1_000_000_000; i++) {
    if (navigator.scheduling?.isInputPending()) {
      await pasue();
    }
  }
}

async function pasue() {
  return new Promise((res) => setTimeout(res));
}
```

<br />

- [ ] on scroll
- [ ] on click
- [ ] on mousemove
- [x] on all of the above
- [ ] never

## 🤔 My Thinking

[isInputPending()](https://developer.mozilla.org/en-US/docs/Web/API/Scheduling/isInputPending)를 사용하면 이벤트 큐에 `input event`가 대기열에 있는지의 여부를 일정 간격으로 사용자에게 제공한다. <br />
페이지 상에서 사용자가 input과 관련되어 어떠한 입력이 대기 중인 경우에 `isInputPending`의 값이 `true`가 되어 pause 함수가 실행될 것이다.

## 🤓 Answer

Using isInputPending() in combination with a yielding mechanism is a great way to get the browser to stop **whatever tasks it's processing so that it can respond to critical user-facing interactions.** That can help improve your page's ability to respond to the user in many situations when a lot of tasks are in flight.

includeContinuous option parameter is a boolean, which is false by default.
If set to true, it indicates that continuous events should be considered when checking for pending input. Continuous events are trusted events (events dispatched by the browser) that are fired successively, such as mousemove, wheel, touchmove, drag, pointermove, and pointerrawupdate.

## 📄 Reference

> https://web.dev/optimize-long-tasks
