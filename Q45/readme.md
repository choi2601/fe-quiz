# Q45. what will be the output?

## ❓ Question

```js
const obj = { prop: null };

obj?.prop = 'hello';

console.log(obj?.prop);
```

- [] `hello`
- [] `null`
- [] `undefined`
- [x] `Error`

## 🤔 My Thinking

옵셔널 체이닝(`?.`) 연산자는 속성을 참조할 경우에 사용되며, 속성에 값을 할당할 때는 사용되지 않는다.

따라서 `obj?.prop = 'hello'`는 유효하지 않은 구문이며, 아래와 같은 SyntaxError를 발생시킬 것이다.

> SyntaxError: Invalid left-hand side in assignment expression.

## 🤓 Answer

Explanation.

The optional chaining (?.) operator accesses an object's property or calls a function.
If the object accessed or function called using this operator is undefined or null,
the expression evaluates to undefined instead of throwing an error.

However, optional chaining not valid on the left-hand side of an assignment:

obj?.prop = 'hello'; // SyntaxError: Invalid left-hand side in assignment

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining
