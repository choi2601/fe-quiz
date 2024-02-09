# Q66. What will be the output?

## ❓ Question

```js
const obj = {
  foo: 1,
  get fooValue() {
    return super.foo;
  },
};

Object.setPrototypeOf(obj, { foo: 2 });

console.log(obj.fooValue);
```

- [] `1`
- [x] `2`
- [] `undefined`
- [] `Error`

## 🤔 My Thinking

`obj` 객체의 `fooValue` getter 함수에서 `return super.foo`를 사용하면, 이는 `obj` 객체의 직접적인 속성이 아닌, 그 프로토타입 체인 상의 속성을 참조한다.

여기서 `super` 키워드는 객체의 프로토타입, 즉 부모 객체의 메서드나 속성에 접근할 때 사용된다.

`Object.setPrototypeOf(obj, {foo: 2})`를 호출함으로써, `obj` 객체의 프로토타입을 새로운 객체 `{foo: 2}`로 설정한다. 그래서 `obj` 객체 자체에는 `foo: 1`이라는 속성이 있지만,

`obj.fooValue` getter를 통해 `super.foo`를 호출하면, `obj`의 프로토타입 체인을 따라가서 발견되는 첫 번째 `foo` 속성의 값을 참조하는 것이다.

## 🤓 Answer

Explanation.

The `super`` keyword can be used in the object literals.
When accessing the super.x, x property is seeked on the object literal/class declaration's prototype.

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf
