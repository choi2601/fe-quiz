# Q83. What will be the output?

## ❓ Question

```js
const obj = {
  logProp() {
    console.log(this.prop, super.prop);
  },
};

Object.setPrototypeOf(obj, { prop: 1 });

const log = obj.logProp;

log();
```

- [] `1 1`
- [] `undefined 1`
- [] `1 undefined`
- [] `undefined undefined`
- [x] `Error`

## 🤓 Answer

Explanation.

super can also be used in the object literals.
Accessing super.x behaves like Reflect.get(Object.getPrototypeOf(objectLiteral), "x", this), which means the property is always seeked on the object literal/class declaration's prototype, and unbinding and re-binding a method won't change the reference of super.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super
