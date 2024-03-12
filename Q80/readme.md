# Q80. What will be the output?

## ❓ Question

```js
function foo(a, b) {
  arguments[1] = 2;
  console.log(b);
}

foo(0, 1);
```

- [] `0`
- [] `1`
- [x] `2`
- [] `Error`

## 🤔 My Thinking

`arguments` 객체는 함수에 전달된 모든 인자를 유사 배열 객체(Array-like)로써 저장한다. 해당 객체 내의 인덱스는 함수에 전달된 인자의 위치를 반영한다.

함수 내에서 arguments 객체의 값을 변경하면, 해당 인자의 값도 변경된다.

하지만 `strict mode`에서는 arguments 객체와 함수 파라미터 사이의 동기화가 이뤄지지 않는다.

arguments 객체는 함수 렉시컬 환경(Function Lexical Environment)의 함수 환경 레코드(Function Environment Recored)에 저장된다.

## 🤓 Answer

Explanation.

Non-strict functions that are passed only simple parameters (that is, not rest, default, or restructured parameters) will sync the value of variables new values in the body of the function with the arguments object, and vice versa.
