# Q46. What will be the output?

## ❓ Question

```js
class A {
  constructor() {
    this.x = 10;
  }
}

A = class B {
  constructor() {
    this.x = 20;
  }
};

console.log(new A().x);
```

- [] `10`
- [x] `20`
- [] `undefined`
- [] `Error`

## 🤔 My Thinking

자바스크립트에서 클래스는 사실상 함수의 한 형태로, 프로토타입 기반 상속을 기반으로 동작한다. ES6에서 도입된 `class` 키워드는 기존의 프로토타입 기반 상속을
보다 명확하고 쉽게 사용할 수 있도록 하는 문법적 설탕(syntatic sugar)이다.

즉, 위의 코드를 다음과 같이 함수 선언문으로 바꿀 수 있다.

```js
function A {
    this.x = 10;
}

A = function B() {
    this.x = 20;
}
```

자바스크립트에서의 함수는 일급 객체로서 값처럼 자유롭게 사용할 수 있기 때문에 재할당 또한 가능하다.

위의 함수 선언문을 다시 아래와 같이 표현한다면 더 이해하기 쉬울 것이다.

```js
var A = function A() {
  this.x = 10;
};

// B는 함수 객체로서 변수 A에 할당된다
A = function B() {
  this.x = 20;
};
```

함수는 함수 이름으로 호출하는 것이 아니라 함수 객체를 가리키는 식별자로 호출한다.
자바스크립트 엔진은 함수 선언문을 함수 표현식으로 변환해 함수 객체를 생성한다고 볼 수 있다.

위와 같은 각 변환 단계를 거쳐 보았을 때 클래스 또한 재할당이 가능하며 this 또한 새로 참조되는 인스턴스를 가리킬 것이다.

## 🤓 Answer

Explanation.

Classes in JavaScript under the hood are special type of functions.

console.log(typeof A); // function

This construct creates a variable A in memory that refers to the function:

class A {
constructor() {
this.x = 10;
}
}

On this line we assign variable A a reference to another function:

A = class B {
constructor() {
this.x = 20;
}
}

console.log(new A().x); // 20

This class expression syntax is valid. Note that, as with function expressions, variable B is not accessible from the outside.

console.log(new B().x); // ReferenceError: B is not defined

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining
