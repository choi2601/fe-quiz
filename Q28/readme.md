# Q28. Which loop will run the faster?

## ❓ Question

```js
const strPrimitive = generateRandomString(100_000);
const strObject = new String(generateRandomString(100_00));

String.prototype.customMethod = (i) => i * i;

console.time("primitive");
for (let i = 0; i < 100_000; i++) {
  strPrimitive.customMethod(i);
}
console.timeEnd("primitive");

console.time("object");
for (let i = 0; i < 100_000; i++) {
  strObject.customMethod(i);
}
console.timeEnd("object");
```

- [] primitive
- [x] object
- [] same time

## 🤔 My Thinking

내장 메서드를 사용할 경우 원시 문자열(primitive string)에 대한 최적화가 자체적으로 이루어지기 때문에 object 타입이 성능 상 더 빠를 것으로 예상이 된다.

## 🤓 Answer

Explanation.

Using built-in methods like slice on a primitive string, engines perform optimization, which is called differently in different engines - short or fast path. The optimization lies in the fact that the engine does not create a wrapper object when accessing a property or method, but immediately performs the required action.

However, for custom methods the fast path is not available, so applying a custom method to a primitive gives worse performance than applying it to an object.

primitive: 5.258ms
object: 1.809ms
