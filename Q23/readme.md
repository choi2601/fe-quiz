# Q23. What will be the output?

## ❓ Question

```js
"use strict";

this.baz = 1;
const cb = () => console.log(this.baz);

const foo = {
  baz: 2,
  bar: function () {
    return cb();
  },
};

foo.bar();
```

- [] 1
- [] 2
- [x] undefined
- [] Error

## 🤔 My Thinking

해당 코드는 strict mode에서 실행되고 있다. strict mode에서 전역 객체에 대한 this는 `undefined`이다. 따라서 `this.baz = 1`는 사실상 무시되며, cb 함수 내부에서 this.baz는 undefined를 반환합니다. 또한, cb는 화살표 함수로 정의되어 있어, this를 렉시컬로 결정한다. 즉, 화살표 함수는 선언될 당시의 this를 캡쳐하며 cb 함수가 전역 스코프에서 선언되었으므로 this는 undefined이다.

## 🤓 Answer

Explanation.

Arrow functions do not bind their own this, instead they inherit it from the parent scope in which they are defined. Our arrow function is defined in the global scope, so this within it refers to the global scope. It doesn't matter where the function is called from.

## 📄 Reference

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions
