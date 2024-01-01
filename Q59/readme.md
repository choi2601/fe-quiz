# Q59. What will be the output?

## ❓ Question

```js
function myFunc() {
  return "hello";
}

const myArrowFunc = () => "hello";

console.log(Object.hasOwn(myFunc.prototype, "constructor"));
console.log(Object.hasOwn(myArrowFunc.prototype, "constructor"));
```

- [] `true true`
- [x] `true false`
- [] `false false`
- [] `Error`

## 🤔 My Thinking

일반함수는 기본적으로 `prototype` 프로퍼티를 가진다. 해당 `prototype` 객체는 `constructor` 속성을 가지며, 해당 속성은 함수 자체를 바인딩한다.
따라서 `Object.hasOwn(myFunc.prototype, "constructor")` 는 `true`를 반환한다.

반면 화살표 함수는 `prototype` 속성을 가지지 않는다. 화살표 함수는 주로 익명 함수로서 사용되며, 일반적으로 생성자 함수로 사용되지 않기 때문이다.
따라서 `myArrowFunc.prototype`은 `undefined`이고, `Object.hasOwn(myArrowFunc.prototype, "constructor")`는 `false`를 반환한다.

추가적으로 설명하자면, 함수 객체만이 소유하는 `prototype` 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킨다. `prototype` 프로퍼티는 생성자 함수가 생성할
객체(인스턴스)의 프로토타입을 가리킨다. 따라서 생성자 함수로서 호출할 수 없는 함수, 즉 `non-constructor`인 화살표 함수와 ES6 메서드 축약 표현으로 정의한 메서드는 `prototype` 프로퍼티를
소유하지 않으며 프로토타입도 생성하지 않는다.

## 🤓 Answer

Explanation.

Javascript automatically creates a prototype object whenever you declare a function:

```js
function MyFunc() {}

console.log(MyFunc.prototype); // {}
```

This object is not empty. It has a constructor property that points back to the function.

```js
console.log(Object.hasOwn(myFunc.prototype, "constructor")); // true
```

When you create a new instance of a function then the function's prototype becomes the new obj.**proto**.

```js
const obj = new MyFunc();

console.log(obj.**proto** === MyFunc.prototype); // true
```

Arrow functions cannot be used as a constructor, therefore they do not have the prototype property.

```js
new myArrowFunc(); // TypeError: myArrowFunc is not a constructor

console.log(Object.hasOwn(myArrowFunc.prototype, "constructor"));
// TypeError: Cannot convert undefined or null to object
```
