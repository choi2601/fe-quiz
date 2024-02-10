# Q67. What will be the output?

## ❓ Question

```js
const square = {
  num: 3,
  pow() {
    return this.num * this.num;
  },
  double: () => 2 * this.num,
};

console.log(square.pow(), square.double());
```

- [] `9, 6`
- [] `9, undefined`
- [] `undefined, undefined`
- [x] `9, NaN`
- [] `9, null`

## 🤔 My Thinking

`pow` 메서드는 일반 함수로 선언되어 있다. 이 경우 `this`는 메서드를 호출한 객체인 `square`를 참조한다. 따라서 `this.num`은 3이 되고 함수의 결과는 9가 된다.

반면 `double` 메서드는 화살표 함수로 선언되어 있다. 화살표 함수는 자신을 포함하는 외부 스코프의 `this` 값을 상속받는다. `double` 함수가 정의된 스코프(전역 스코프 혹은 해당 스크립트의 최상위 스코프)에서 `this`는
`square` 객체를 참조하지 않기 때문에 NaN의 결과가 된다. 이는 전역 스코프에서의 `this`는 전역 객체(window, global)를 가리키거나, 엄격 모드(use strict)에서는 `undefined`가 되기 때문이다.

## 🤓 Answer

Explanation.

Both functions are called with the square object being passed as the context.
However, arrow functions do not have their own this, so the passed context will be ignored. Instead, they use the context of the outer function. In this case, the external context is the global object. There is no num variable in the global object, so this.num has the value undefined.

JS automatically casts operands to numbers in mathematical operations -, /, _. Number(undefined) = NaN; number _ NaN = NaN
