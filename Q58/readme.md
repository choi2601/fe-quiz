# Q58. What will be the output?

## ❓ Question

```js
function myFunc() {}

console.log(Object.getPrototypeOf(myFunc.prototype));
```

- [] `Function.prototype`
- [x] `Object.prototype`
- [] `null`
- [] `Error`

## 🤔 My Thinking

`myFunc`은 자바스크립트에서 함수 객체이다. 자바스크립트에서 모든 함수 객체는 기본적으로 `prototype` 속성을 가진다. 해당 `prototype` 객체의 프로토타입은
`Object.prototype` 이다.

`Object.getPrototypeOf(myFunc.prototype)`은 `myFunc.prototype`의 프로토타입을 반환한다. 모든 일반 객체의 기본 프로토타입은 `Object.prototype`이므로,
`Object.prototype`을 반환할 것이다.

## 🤓 Answer

Explanation.

Javascript automatically creates a prototype object whenever you declare a function:

```js
function MyFunc() {}

console.log(MyFunc.prototype); // {}
```

**This object is not empty. It has a constructor property that points back to the function.**

**The constructor property is usually not printed by the console API, because it is not enumerable.**

```js
console.log(Object.getOwnPropertyDescriptors(MyFunc.prototype));

// {
// constructor: {
// value: [Function: MyFunc],
// writable: true,
// enumerable: false,
// configurable: true
// }
// }
```

But you still can access it:

```js
console.log(MyFunc.prototype.constructor); // [Function: MyFunc]
```

You can also extend an object with your own properties.

```js
console.log(MyFunc.prototype.constructor); // [Function: MyFunc]
```

```js
console.log(MyFunc.prototype); // { sayHello: [Function (anonymous)] }
```

When you create a new instance of a function then the function's prototype becomes the new obj.**proto**.

```js
const obj = new MyFunc();

console.log(obj.**proto** === MyFunc.prototype); // true
```

Another way to get the **proto** of an object is to use the Object.getPrototypeOf() method.

```js
console.log(obj.**proto** === Object.getPrototypeOf(obj)); // true
```

So the expression Object.getPrototypeOf(MyFunc.prototype) means: get the object that was used to create MyFunc.prototype.

Because MyFunc.prototype is an object, its prototype is Object.prototype.

```js
console.log(
Object.getPrototypeOf(MyFunc.prototype) === Object.prototype,
MyFunc.prototype.**proto** === Object.prototype
); // true true
```

And the prototype of MyFunc is Function.prototype:

```js
console.log(Object.getPrototypeOf(MyFunc) === Function.prototype); // true
```
