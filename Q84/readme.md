# Q84. What will be the output?

## ❓ Question

```js
const [x, ...{ length }] = [1, 2, 3];

console.log(length);
```

- [] `1`
- [x] `2`
- [] `3`
- [] `undefined`
- [] `Error`

## 🤔 My Thinking

객체 구조 분해 할당(Object Destructuring Assignment)은 배은 객체에도 적용될 수 있다.

배열 역시 JavaScript에서는 객체의 한 형태이며, 배열 객체는 length라는 속성을 가지고 있다.

위의 문제 코드를 풀어보면 다음과 같다.

```js
const [x] = [1];

// 배열 또한 인덱스를 키로 가진 객체이기 때문에 구조 분해 할당 시 객체 리터럴 형태로 할당 받을 수 있다.
const { 0: a, 1: b, length } = [2, 3];

// 1
console.log(x);

// 2, 3
console.log(a, b);
// 2
console.log(length);
```

## 🤓 Answer

Explanation.

The rest property of array destructuring assignment can be another array or object.
The inner destructuring destructures from the array created after collecting the rest elements.

```js
const [x, ...{ length }] = [1, 2, 3];
```

is equivalent to

```js
const [x] = [1, 2, 3]; // 1
const { length } = [2, 3]; // 2
```

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
