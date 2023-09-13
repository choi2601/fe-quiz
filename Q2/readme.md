# Q2. Event listener of which element is more efficient?

## ❓ Question

```js
foo.addEventListener(
  "touchstart",
  (event) => {
    console.log("foo");
  },
  { passive: true }
);

bar.addEventListener(
  "touchstart",
  (event) => {
    console.log("bar");
  },
  { passive: false }
);
```

<br />

- [x] foo
- [ ] bar
- [ ] equally

## 🤔 My Thinking

addEventListener 옵션 중 `passive`의 기본값은 **_false_** 이다. 값이 **_false_** 일 경우에 touchstart, touchmove와 같은 이벤트가 발생하면 preventDefault를 이용하여 실제 이벤트 자체를 막을 수 있기 때문에, 브라우저는 이벤트 동작을 계속 감시해야 한다. <br />
**_true_** 를 설정할 경우 preventDefault를 절대 호출하지 않을 것임을 보장하기 때문에 사용자가 스크롤을 할 시, 브라우저의 렌더링을 방해하지 않아 더 나은 스크롤 성능을 기대할 수 있다.

## 🤓 Answer

Touch and wheel event listeners can delay page scrolling.

Browsers can't know if an event listener will prevent scrolling using event.preventDefault(), so they always wait for the listener to finish executing before scrolling the page.

Passing the { passive: true } option to the event listener solve this problem by letting you indicate that the event listener will never call the event.preventDefault().

## 📄 Reference

> https://developer.chrome.com/docs/lighthouse/best-practices/uses-passive-event-listeners/

> https://developer.mozilla.org/ko/docs/Web/API/Event/preventDefault

> https://developer.mozilla.org/ko/docs/Web/API/EventTarget/addEventListener#%ED%8C%A8%EC%8B%9C%EB%B8%8C_%EC%88%98%EC%8B%A0%EA%B8%B0%EB%A1%9C_%EC%8A%A4%ED%81%AC%EB%A1%A4_%EC%84%B1%EB%8A%A5_%ED%96%A5%EC%83%81
