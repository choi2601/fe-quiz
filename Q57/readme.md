# Q57. What will be the output?

## ❓ Question

```js
const foo = {
    hello: () => console.log("hello");
}

const bar = Object.create(foo);
const baz = Object.create(bar);

console.log("hello" in bar);
console.log("hello" in baz);
```

- [x] `true true`
- [] `true false`
- [] `false true`
- [] `false false`

## 🤔 My Thinking

`Object.create` 메서드는 새로운 객체를 생성하고, 인자로 전달된 객체를 새로 생성된 객체의 프로토타입으로 생성한다.

`const bar = Object.create(foo);`는 `foo`를 `bar`의 프로토타입으로 설정하고 `const baz = Object.create(bar);`는 `bar`를 `baz`의 프로토타입으로
설정한다.

`"hello" in bar` 표현식은 "hello" 라는 속성이 `bar` 객체 또는 그 프로토타입 체인 상에서 존재하는지 확인한다. `bar`의 프로토타입은 `foo`이고, `foo`에는 `hello` 속성이 있으므로
해당 표현식으로 `true`를 반환한다. 마찬가지로 `baz` 또한 프로토타입 체인에 `bar`를 포함하고, `bar`의 프로토타입은 `foo`이므로 `hello` 속성이 존재한다.

## 🤓 Answer

Explanation.

The Object.create() static method creates a new object, using an existing object as the prototype of the newly created object.

console.log(Object.getPrototypeOf(bar)); // { hello: [Function: hello] }

console.log(Object.getPrototypeOf(baz)); // {} (bar object)

console.log(Object.getPrototypeOf(baz.**proto**)); // { hello: [Function: hello] }

The in operator returns true if the specified property is in the specified object or its prototype chain.

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create

> https://velog.io/@thms200/Object.create-
