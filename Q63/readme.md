# Q63. What will be the output?

## ❓ Question

```js
"use strict";

const user = {
  name: "Alex",
  printUser: () => {
    return `User: ${this.name}`;
  },
};

console.log(user.printUser());
```

- [] `User: Alex`
- [x] `User: undefined`
- [] `Error`

## 🤔 My Thinking

자바스크립트에서 화살표 함수는 자신만의 this 컨텍스트를 생성하지 않는다. 대신, 화살표 함수는 자신이 선언된 렉시컬 스코프의 this 값을 사용한다. 이 경우 printUser 메서드는 객체 리터럴 내에서 정의되었지만, 화살표 함수는 외부 스코프(가장 가까운 일반 함수 또는 전역 스코프)의 this 값을 사용한다.

이 코드에서 printUser는 전역 스코프(global scope)에서 실행되므로 this는 전역 객체(브라우저에서는 window, Node.js에서는 global)를 가리키게 된다.

이 경우 user 객체에 정의된 name 속성은 전역 객체에 존재하지 않으므로 this.name은 undefined를 반환한다. 따라서 출력값은 `User: undefined`이 된다.

만약 this의 값이 객체 리터널 내 name 값을 사용하고 싶다면 일반 함수를 사용하거나 의도적으로 this 바인딩을 하면 된다.

```js
"use strict";

const user = {
  name: "Alex",
  printUser: function () {
    return `User: ${this.name}`;
  },
};

// User: Alex
console.log(user.printUser());
console.log(user.printUser.call(user));
```

## 🤓 Answer

Explanation.

Arrow functions do not have their own context, so calling an arrow function as a method on an object does not set the this value inside the arrow function to a reference to that object. Instead, the arrow function will inherit the this value from its parent function. The user object, which has an arrow function as its method, is in the global scope. The value of this in the global scope is a reference to the global object. This is also true in strict mode.

The results of this example may vary depending on the environment in which you run the code. In node.js you will get `User: undefined` because the name property is not defined in the global object. In the browser, the global object is window, which has a name property set to the empty string by default, so the result will be `User:`

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch
