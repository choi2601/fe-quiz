# Q85. Which will be the output?

## ❓ Question

```js
function sum(obj1, obj2) {
  return obj1?.x + obj2?.y;
}

console.log(sum({ x: 5 }))
```

- [] `5`
- [x] `NaN`
- [] `undefined`
- [] `Error`

## 🤔 My Thinking

함수 내부에서 `obj?.x`는 5가 되지만, `obj2?.y`는 'undefined`가 된다.

JavaScript에서 `undefined`를 더하면 `NaN`이 된다.

## 🤓 Answer

Explanation.

The optional chaining (?.) operator accesses an object's property or calls a function.
If the object accessed or function called using this operator is undefined or null,
the expression evaluates to undefined instead of throwing an error.

Number(undefined) is NaN.
