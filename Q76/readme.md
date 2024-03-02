# Q76. What will be the output?

## ❓ Question

```js
const arg1 = Symbol(2);
const arg2 = Symbol(3);

console.log(arg1 + arg2);
```

- [] `5`
- [] `Symbol(2)Symbol(3)`
- [] `NaN`
- [x] `Error`

## 🤔 My Thinking

JavaScript의 `Symbol`은 유일하고 변경 불가능한 원시 데이터 타입으로, 주로 객체 속성의 키로 사용된다.

`Symbol`은 다른 어떤 심볼 값과도 동일하지 않다. 즉, 동일한 문자열이나 숫자를 가진 두 심볼을 생성하더라도 이들은 서로 다른 심볼로 취급된다.

`Symbol` 타입에 대해 신술 연산자를 사용할 경우, JavaScript는 `TypeError`를 발생시킨다.

## 🤓 Answer

Explanation.

When trying to convert a Symbol to a number, a TypeError will be thrown:

TypeError: Cannot convert a Symbol value to a number

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol
