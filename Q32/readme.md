# Q32. How many times will the ResizeObserver callback be called?

## ❓ Question

```js
const el = document.getElementById('box');
const body = document.body;

let i = 1;
const observer = new ResizeObserver((entries) => {
    const curFontSize = getComputedStyle(body).fontSize;
    body.style.fontSize = parseInt(curFontSize) + i + 'px';
    i++;
})

observer.observe(el);
```

- [] 0
- [] 1
- [x] infinity
- [x] until the ResizeObserver loop limit is exceeded
- [] until the element stops growing

## 🤔 My Thinking

특정 엘리먼트의 크기가 body 요소의 fontSize 변경에 반응한다는 것이 확실하다면 ResizeObserver 콜백은 계속 호출될 것이다. <br />
또한 ResizeObderver의 루프 보호 장치에 의해 연속해서 일정 횟수 이상의 콜백 호출이 발생할 경우 이를 방지하기 위한 *ResizeObserver loop limit exceeded* 오류가 발생할 수도 있다.

## 🤓 Answer

Explanation.

The ResizeObserver interface reports changes to the dimensions of an Element's content or border box.

In the example, changing the body font size causes the element to increase in size, causing the callback to be called again and again.

**Browsers have an upper limit on font sizes, so at some point in time, changing the font size will no longer make the element larger (1000px on my device). Then the ResizeObserver callback will no longer be called.**

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver