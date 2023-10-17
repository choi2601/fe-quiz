# Q25. Which array cloning is the fastest?

## ❓ Question

```js
function clone(arr) {
  const result = new Array(arr.length);
  for (let i = 0; i < arr.length; i++) {
    result[i] = arr[i];
  }
  return result;
}

const origin = new Array(10_000);
for (let i = 0; i < origin.length; i++) {
  origin[i] = Math.random();
}

const manualClone = clone(origin);
const sliceClone = origin.slice();
const spreadClone = [...origin];
```

- [] manual
- [] slice
- [] spread
- [] same time

## 🤔 My Thinking

성능은 실행 환경, JavaScript 엔진, 그리고 다른 여러 요소에 따라 다르기 때문에 절대적인 정답을 주기는 어렵다.

## 🤓 Answer

Explanation.

Cloning using the slice method is the fastest.

In V8 since version v7.2 / Chrome 72, which introduced optimizations, and in Safari, using the spread operator to clone an array catches up with slice in speed. In Safari and v8 applying to small arrays of up to 1000 elements it even outperforms.

Performing a manual clone is the slowest cloning method in all browsers.

Cloning an array with 100_000 elements:

v8:

manual: 2.685ms
slice: 0.473ms
spread: 0.673ms

Safari:

manual: 2.025ms
slice: 1.302ms
spread: 0.490ms

Firefox:

manual: 3ms
slice: 1ms
spread: 3ms

However, let me remind you that all optimizations of built-in functions and operators only work for real arrays. For pseudo-arrays, manual cloning will always be faster, since dynamic optimizations will be applied to it for a large number of operations.

class CustomArray extends Array{}
const origin = new CustomArray(100_000);

Cloning CustomArray in V8:

manual: 3.145ms
slice: 16.731ms
spread: 8.867ms
