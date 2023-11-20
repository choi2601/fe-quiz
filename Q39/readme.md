# Q39. What will be the output?

## ❓ Question

```js
const arr = [1, 2, 3];

console.log(3 in arr);
```

- [] true
- [x] false
- [] undefined
- [] Error

## 🤔 My Thinking

`in` 연산자는 객체의 속성이 존재하는지를 검사한다. 자바스크립트에서의 배열은 객체이며 배열에서 in 연산자는 배열의 인덱스가 존재하는지 검사한다.

주어진 배열 arr은 인덱스가 0, 1, 2까지 존재하기 때문에 false를 반환할 것이다.

## 🤓 Answer

Explanation.

The in operator returns true if the specified property is in the specified object or its prototype chain.

Because arr[3] is not defined:

console.log(3 in arr); // false

Checking if a property exists with the in operator can be useful when your array may contain undefined:

const arr = [1, 2, 3, undefined];

console.log(!!arr[3]); // false
console.log(3 in arr); // true

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in
