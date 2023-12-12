# Q55. What will be the output?

## ❓ Question

```js
const obj = { foo: {} };

const copy1 = { ...obj };
const copy2 = structuredClone(obj);

obj.foo.bar = "baz";

console.log(copy1.foo.bar, copy2.foo.bar);
```

- [] `baz baz`
- [] `baz undefined`
- [] `undefined baz`
- [] `undefined undefined`
- [] `Error`

## 🤔 My Thinking

현재 obj를 얕은 복사(shallow copy)와 깊은 복사(depp copy)를 사용해 복제하고 있다.

1. `{...obj}`는 스프레드 연산자를 사용한 얕은 복사를 수행한다. 이 경우 `obj`의 최상위 속성만 복사하며, 중첩된 객체는 참조(기존 메모리 주소값)로 복사된다.
2. `structuredClone(obj)`는 깊은 복사를 수행한다. 이 경우 `obj`의 모든 중첩된 객체를 포함하여 새로운 독립적인 복제본(새로운 메모리 주소값)을 생성한다.

따라서 `console.log(copy1.foo.bar, copy2.foo.bar);`의 결과는 baz (얕은 복사된 객체에서)와 undefined (깊은 복사된 객체에서 foo 객체에는 bar 속성이 없음)가 된다.

## 🤓 Answer

Explanation.

Cloning objects using ...spread as well as Object.assign we only get shallow copies:
If one of the original property values is an object, the clone will refer to the same object, it will not be recursively cloned itself.

The global structuredClone() method creates a deep clone of a given value.
