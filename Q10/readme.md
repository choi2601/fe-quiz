# Q10. What time will be less?

## ❓ Question

```js
const elements = [...document.querySelectorAll(".box")];

console.time("A");
elements.forEach((element) => element.classList.add("some-class"));
const rects = elements.map((element) => element.getBoundingClientRect());
console.timeEnd("A");

console.time("B");
for (let i = 0; i < elements.length; i++) {
  elements[i].classList.add("some-class2");
  const rect = elements[i].getBoundingClientRect();
}
console.timeEnd("B");
```

- [ ] A
- [ ] B
- [x] roughly equivalent

## 🤔 My Thinking

옵션 A와 B는 순회하는 횟수가 다르다. 하지만 이는 미비한 경우이고 실제 DOM에 접근하는 횟수는 동일하다. <br />
DOM 접근은 일반적인 자바스크립트 연산보다 느리기 때문에 요소의 수가 작다면 두 반복문 차이엔 크게 의미가 없을 것이다.

## 🤓 Answer

Explanation.

Before moving on to painting elements on the page, the browser needs to calculate the compute styles and coordinates for each element. This process is called reflow.

JavaScript has APIs for getting information about the dimensions and coordinates of an element on the page at the current time. One of such methods is getBoundingClientRect().

The Element.getBoundingClientRect() method returns a DOMRect object providing information about the size of an element and its position relative to the viewport.

**Such methods can be very inefficient because the browser does not always have the required information about the element.**

For example, by doing the operation

```js
element.classList.add("some-class");
```

we could change its dimensions, coordinates, and also affect its descendants. So when we next ask the browser to return the actual information about the element

```js
element.getBoundingClientRect();
```

**the browser needs to perform an expensive reflow operation.**

When we write and then read in a loop, at each iteration the browser must perform a reflow. To optimize such a task, it is better to first write to all elements, and then read.
This way the browser can do the same with only one reflow.

Difference in time for 100 elements:

A: 0.8 ms
B: 12.2 ms

## 📄 Reference

> https://www.webperf.tips/tip/layout-thrashing/

> https://developer.mozilla.org/ko/docs/Web/API/Element/getBoundingClientRect
