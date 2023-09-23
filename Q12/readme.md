# Q12. What will you see on the screen?

## ❓ Question

```js
setTimeout(() => (document.body.innerHTML = "A"));

requestAnimationFrame(() => (document.body.innerHTML = "B"));

setTimeout(() => (document.body.innerHTML = "C"));

document.body.innerHTML = "D";
```

- [ ] A
- [ ] B
- [x] C
- [ ] D

## 🤔 My Thinking

초기에 `document.body.innerHTML = "D"`가 실행되어 내용이 D로 설정된다. <br />
이후 이벤트 루프 상 첫 번째 setTimeout callback이 큐에서 콜 스택(call stack)으로 참조되어 내용이 A로 변경된다. <br />
requestAnimationFrame 같은 경우는 일반적으로 렌더링 시퀀스가 실행되기 직전에 실행이 되므로 이때 내용이 B로 변경된다. <br />
마지막으로, 두 번째 setTimeout이 실행되어 내용이 C로 변경이 된다.

## 🤓 Answer

Explanation.

The requestAnimationFrame callback is called just before rendering, after the task (e.g the execution of a setTimeout callback) is completed.

**According to the event loop algorithm, rendering can happen after each task is executed. However, the browser may skip this step. In the example, the browser concatenates setTimeout with the same timer values ​​and skip rendering after script execution. Therefore, the user will immediately see B on the screen.**

===

**Indeed, callbacks will be called in this order. However, because the browser sometimes skips the rendering step, we won't see D, A, and C on the screen. If you go to chrome dev tools -> performance , you'll see that there was only one frame. The one that contains B.**

If the browser had not optimized and skipped rendering steps, we would have seen the following order: DBAC . The first render would have happened after the script was executed, and the call to requestAnimationFrame would have happened before that render. As a result, we would see a different result on the page - C. This is how Safari works now.

Therefore, to achieve a consistent result, if we want the requestAnimationframe to be executed after the setTimeout call, we need to put it inside this call.
