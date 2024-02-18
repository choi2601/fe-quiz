# Q71. What will be the output?

## ❓ Question

```js
let bar = function foo() {
  return new Object();
};

console.log(bar() === foo());
```

- [] `true`
- [] `false`
- [] `Error`

## 🤔 My Thinking

`foo`는 함수 내부에서만 접근 가능한 이름이다. 즉, 함수 외부에서는 foo를 직접 호출할 수 없다.

`console.log(bar() === foo())`를 실행한다면, foo 함수가 현재 스코프에서 정의되지 않았기 때문에 `ReferenceError`가 발생한다.

foo는 bar 변수에 할당된 함수 표현식의 이름으로, 이 이름은 위에서 말한 것과 같이 함수 외부에선 접근할 수 없기 때문이다.

```js
// 기명 함수 리터럴을 단독으로 사용하면 함수 선언문으로 해석된다.
// 함수 선언문에서는 함수 이름을 생략할 수 없다.
function foo() {
  console.log("foo");
}

foo()(
  // foo

  // 함수 리터럴을 피연산자로 사용하면 함수 선언문이 아니라 함수 리터럴 표현식으로 해석된다.
  // 함수 리터럴에서는 함수 이름을 생략할 수 있다.
  function bar() {
    console.log("bar");
  }
);

bar(); // ReferenceError: bar is not defined
```

그룹 연산자의 피연산자는 값으로 평가될 수 있는 표현식이어야 한다. 따라서 표현식이 아닌 문인 함수 선언문은 피연산자로 사용할 수 없다.

이처럼 이름이 있는 기명 함수 리터럴은 코드의 문맥에 따라 함수 선언문 또는 함수 리터럴 표현식으로 해석된다.

자바스크립트 엔진은 생성된 함수를 호출하기 위해 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고, 거기에 함수 객체를 할당한다.

즉, 함수는 함수 이름으로 호출하는 것이 아니라 함수 객체를 가리키는 식별자로 호출한다.

결론적으로 JavaScript 엔진은 함수 선언문을 함수 표현식으로 변환해 함수 객체를 생성한다고 생각할 수 있다.

## 🤓 Answer

Explanation.

There are different ways to create a function in JavaScript. These methods include function declaration

function foo() {}

and function expression

let bar = function () {}

The value in a function expression can be either an anonymous function or a named one.

let bar = function () {}

console.log(bar.name); // bar

let bar = function foo() {}

console.log(bar.name); // foo

However, in a named function expression, you can only access the function by name from within it.

let bar = function foo () {
console.log(foo); // [Function: foo]
return new Object();
}

bar();

console.log(foo); // ReferenceError: foo is not defined
