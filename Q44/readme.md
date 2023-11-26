# Q44. What will be the output?

## ❓ Question

```js
const foo1 = Symbol.for("foo");
const foo2 = Symbol.for("foo");

console.log(foo1 === foo2);
```

- [x] `true`
- [] `false`
- [] `undefined`
- [] `Error`

## 🤔 My Thinking

전역 심볼 레지스트리(Global Symbol Registry)는 JavaScript에서 모든 심볼(Symbol) 값들이 저장되는 시스템이다. <br />
심볼은 JavaScript의 고유한 데이터 타입으로, 주로 객체 속성의 키로 사용된다. 각 심볼은 고유하며, 동일한 이름으로 여러 번 생성하여도 서로 다른 값을 가진다.

```js
Symbol("foo") === Symbol("foo"); // false
```

그러나 `Symbol.for` 메서드를 사용하면, 전역 심볼 레지스트리를 통해 심볼을 생성하고 접근할 수 있다. 해당 메서드는 주어진 문자열을 키로 사용하여 심볼을 찾는다. <br />
해당되는 문자열 키가 이미 레지스트리에 존재하면, 해당 심볼을 반환하며 존재하지 않을 경우엔 새로운 심볼을 생성하고 레지스트리에 추가한 후 반환한다.

## 🤓 Answer

Explanation.

The Symbol.for() static method searches for existing symbols in a runtime-wide symbol registry with the given key and returns it if found. Otherwise a new symbol gets created in the global symbol registry with this key.

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/for
