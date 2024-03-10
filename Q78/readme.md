# Q78. What will be the output?

## ❓ Question

```js
"use strict";
var x = 5;
var y = 5;

function Operations(op1 = x, op2 = y) {
  this.x = op1;
  this.y = op2;
}

Operations.prototype.sum = () => this.x + this.y;

const op = new Operations(10, 20);

console.log(op.sum());
```

- [] `30`
- [] `10`
- [] `undefined`
- [x] `NaN`
- [] `Error`

## 🤔 My Thinking

화살표 함수의 `this`는 자신이 선언된 함수 범위를 가리키지 않고, 선언된 시점의 `this` 컨텍스트를 유지한다.

이 경우 전역 this를 가리키게 되는데, `use strict` 모드가 활성화되어 있기 때문에, 전역 this는 `undefined`가 된다.

`undefined.x + undefined.y`는 `NaN(Not-a-Number)` 결과를 산출한다.

## 🤓 Answer

Explanation.

Arrow functions don't have their own this. Instead this inside an arrow function's body points to the this value into the scope the arrow function is defined within.

Our function is defined in the global scope.

this in global scope refer to the global object (even in strict mode).
