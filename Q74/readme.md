# Q74. What will be the output?

## ❓ Question

```js
function sum(obj1, obj2) {
  return obj1?.x + obj2?.y;
}

console.log(sum({ x: 5 }));
```

- [] `5`
- [x] `NaN`
- [] `undefined`
- [] `Error`

## 🤔 My Thinking

선택적 체이닝 연산자(optional chaining) 연산자는 해당 객체나 속성이 `undefined` 또는 `null`일 경우, 오류를 발생시키지 않고, undefined를 반환한다.

`obj?.y`는 obj2가 undfined이므로 결과적으로 `undefined * 5`가 수행되어, `NaN`을 결과로 반환한다.

## 🤓 Answer

Explanation.

The optional chaining (?.) operator accesses an object's property or calls a function.
If the object accessed or function called using this operator is undefined or null,
the expression evaluates to undefined instead of throwing an error.

Number(undefined) is NaN.
