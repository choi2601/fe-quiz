# Q11. Which function takes the longest time between call?

## ❓ Question

```js
function timer() {
  for (let i = 0; i < 10_000_000; i++) {}
  setTimeout(timer, 100);
}
timer();

function interval() {
  for (let i = 0; i < 10_000_000; i++) {}
}
setInterval(interval, 100);
```

- [ ] timer
- [x] interval
- [ ] equally

## 🤔 My Thinking

timer 함수에서는 setTimeout이 루프 실행이 끝난 후 동기적으로 호출되며, 그 다음 timer를 다시 호출하기 전에 추가 100밀리초를 기다린다. <br />
반면 interval 함수에서는 setInterval이 루프 실행 시간에 상관 없이 다음 interval 호출을 100밀리초마다 예약한다. <br /> 이때 루프의 실행 시간이 100밀리초 이상일 경우 <br />
다음 interval 함수 호출이 현재 실행이 끝난 직후에 즉시 큐에 적재됨을 의미하기 때문에 호출 사이에 더 적은 시간이 소비된다.

## 🤓 Answer

Explanation.

setInterval calls function in given interval. For example, if the given interval is 100ms, it means that function is called every 100ms.

**If the previous call took 70ms, then the next call will occur after 30ms from the moment it ends (assuming the engine has no more urgent tasks).**

On the other hand, the nested setTimeout ensures that until our method is fully executed, it will not be sent to another execution.

## 📄 Reference

> https://dev.to/moyedx3/10-settimeout-setinterval-and-requestanimationframe-1io4
