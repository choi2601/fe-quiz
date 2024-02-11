# Q68. What will be the output?

## ❓ Question

```js
console.log(String("Hello") === "Hello");
console.log(new String("Hello") === "Hello");
```

- [] `true true`
- [x] `true false`
- [] `false true`
- [] `false false`

## 🤔 My Thinking

`String` 함수는 전달된 값을 문자열 타입으로 변환하고, `new` 키워드 없이 사용되었기 때문에 문자열 리터럴을 반환한다.

반면에 `new` 키워드를 사용하여 `String` 객체를 생성한 경우, 문자열 내용은 `"Hello"`이지만, 문자열 객체를 생성한다.

JavaScript에서 객체와 원시 타입은 엄격한 동등 비교에서 서로 다르게 평가된다.

## 🤓 Answer

Explanation.

JavaScript distinguishes between String objects and primitive string values.
String literals (denoted by double or single quotes) and strings returned from String calls in a non-constructor context (that is, called without using the new keyword) are primitive strings. The value returned by the String constructor is an object.

console.log(typeof new String('hello')); // object
console.log(typeof String('hello')); // string
console.log(typeof 'hello'); // string
