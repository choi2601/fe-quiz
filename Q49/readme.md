# Q49. What will be the output?

## ❓ Question

```js
class Counter {
  #counter = 0;

  constructor() {}

  then(res) {
    res(this.#counter++);
  }
}

const counter = await new Counter();

console.log(counter);
```

- [x] `0`
- [] `1`
- [] `Foo {}`
- [] `NaN`
- [] `Error`

## 🤔 My Thinking

`Counter` 클래스는 비공개 필드 `#counter` 와 `then` 메서드를 가지고 있다.

then 메서드는 `await` 키워드와 함꼐 사용할 수 있도록 클래스를 `thenable` 객체로 만든다. `thenable` 객체는 then 메서드를 가지는 객체로서, `Promise` 와 유사하게 then 구현하여 await 표현식에서 사용할 수 있다.

`const counter = await new Counter()`는 Counter의 인스턴스를 생성하고, await는 then 메서드를 호출한다. then 메서드는 `this.#counter++`를 반환 값으로

사용하므로 후위 연산자에 의해 필드의 현재 값인 0을 반환할 것이다.

## 🤓 Answer

Explanation.

await works with any “thenable”, i.e. any object with a then method, even if it’s not a real promise.

If used postfix (for example, x++), the increment operator increments and returns the value before incrementing.

## 📄 Reference

> https://v8.dev/blog/fast-async
