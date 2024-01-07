# Q61. What will be the output?

## ❓ Question

```js
let x = 5;
let y = (x++, x + 5);

console.log(y);
```

- [] `5`
- [] `6`
- [] `10`
- [x] `11`
- [] `Error`

## 🤔 My Thinking

쉼포 연산자(,)는 각 피연산자를 왼쪽에서 오른쪽으로 평가하고 마지막 피연산자의 결과 값을 반환한다.

```js
let x = 1;

// Expected output: 2
x = (x++, x);

x = (2, 3);

// Expected output: 3
console.log(x);
```

## 🤓 Answer

Explanation.

The comma (,) operator evaluates each of its operands (from left to right) and returns the value of the last operand.

In the example, the first expression increases x by one. The second expression then adds 5 to x and assigns the resulting value to the y. The result is y = 11.

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comma_operator
