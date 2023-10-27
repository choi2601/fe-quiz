# Q29. What will be the output?

## ❓ Question

```js
const obj = {foo: {}};

const copy1 = {...obj};
const copy2 = {structuredClone(obj)};

obj.foo.bar = 'baz';

console.log(copy1.foo.bar, copy2.foo.bar);
```

- [] baz baz
- [x] baz undefined
- [] undefined baz
- [] undefined undefined
- [] Error

## 🤔 My Thinking

`{ ...obj }`는 얕은 복사(shallow copy)를 수행한다. 이로인해 copy1.foo는 obj.foo와 동일한 객체를 참조하게 되므로 `obj.foo.bar = 'baz'`라고 설정하면 `copy1.foo.bar`도 baz가 된다. <br />
반면에 `structuredClone(obj)`는 깊은 복사(deep clone)를 수행한다고 가정하엿을 경우, copy2.foo는 obj.foo의 복사본이므로 `obj.foo.bar = 'baz'`의 복사본이므로 이에 영향을 받지 않는다.

## 🤓 Answer

Explanation.

Cloning objects using ...spread as well as Object.assign we only get shallow copies:
If one of the original property values is an object, the clone will refer to the same object, it will not be recursively cloned itself.

The global structuredClone() method creates a deep clone of a given value.
