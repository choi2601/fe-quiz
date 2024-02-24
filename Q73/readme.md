# Q73. What will be the output?

## ❓ Question

```js
function adjustNumber(num) {
  return Number(num) * 0.01;
}

console.log(typeof adjustNumber("foo"));
```

- [] `string`
- [x] `number`
- [] `object`
- [] `Error`

## 🤔 My Thinking

JavaScript에서 `NaN`은 *Not-a-Number*의 약자로, 숫자가 아님을 나타내는 특별한 값인다.

NaN은 `Number` 타입에 속한다. NaN은 수학적 연산을 수행할 때, 연산의 결과가 유효한 숫자가 아닐 경우 반환된다.

## 🤓 Answer

Explanation.

Number('foo') returns NaN. Despite being "Not-A-Number" typeof NaN === "number".
