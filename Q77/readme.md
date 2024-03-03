# Q77. What will be the output?

## ❓ Question

```js
const x = new Boolean(false);

if (x) {
  console.log("if", x === false);
} else {
  console.log("else", x === false);
}
```

- [] `if true`
- [x] `if false`
- [] `else true`
- [] `else false`

## 🤔 My Thinking

x는 `new Boolean(false)`를 통해 생성된 `Boolean`객체이다. JavaScript에서 `new Boolean(false)`으로 생성된 객체는, 그 내부 값이 `false`일지라도

그 자체로는 진리값(truthy)으로 평가된다. 즉, 객체는 내용에 상관없이 항상 참으로 취급되기 때문에 `if(x)`조건은 참으로 평가된다.

`x === false`비교에서는 x가 `Boolean`객체이고, `false`가 기본 타입의 불리언 값이기 때문에, 이 비교는 항상 `false`를 반환한다.

객체와 기본 타입 값 사이의 엄격한 비교(`===`)는 타입이 다를 때 `false`를 반환한다.

## 🤓 Answer

Explanation.

The condition in the if statement evaluates to true.
Any object, including a Boolean object whose value is false, evaluates to true when passed to a conditional statement.

But truthiness is not the same as being loosely equal to true or false.
x is truthy, but it's also loosely equal to false.
When comparing with false, which is a primitive, x is also converted to a primitive, which is false.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean
