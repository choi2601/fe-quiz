# Q54. What will be the output?

## ❓ Question

```js
const [a, ...x] = "Hello";
console.log(x);

const [b, ...y] = 1234;
console.log(y);
```

- [] `['e', 'l', 'l', '0'], [2, 3, 4]`
- [] `Error, [2, 3, 4]`
- [x] `['e', 'l','l', 'o'], Error`
- [] `Error, Error`

## 🤔 My Thinking

`1234`는 이터러블(iterable)이 아니기 때문에 스프레드 문법을 사용할 수 없다.

ES6에서 도입된 이터레이션 프로토콜(iteration protocol)은 순회 가능한 데이터 컬렉션(자료구조)을 만들기 위해 ECMAScript 사양에 정의하며 미리 약속한 규칙이다.

`String`은 빌트인 이터러블로서 `String.prototype[Symbol.iterator]` 메서드를 호출하게 될 경우 이터레이터 프로토콜을 준수한 이터레이터를 반환하며, `for ... of문`, `스프레드 문법`,
`배열 디스트럭처링 할당` 기능을 사용할 수 있다.

## 🤓 Answer

Explanation.

The array destructuring syntax only works with iterable objects—objects that implement the iterable protocol. Strings are iterable, numbers are not.

// TypeError: 1234 is not iterable

Unlike array destructuring, object destructuring can work with almost any right-hand side, with the exception of null and undefined.

const { a, b } = obj;
// is equivalent to:
// const a = obj.a;
// const b = obj.b;

const { b, ...y } = 1234;
console.log(b); // undefined

The rest operator in this case collects all the remaining properties into a new object.

console.log(y); // {}
console.log('toString' in y); // true

## 📄 Reference

> [이터러블-이터레이터 완벽 이해](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%9D%B4%ED%84%B0%EB%9F%AC%EB%B8%94-%EC%9D%B4%ED%84%B0%EB%A0%88%EC%9D%B4%ED%84%B0-%F0%9F%92%AF%EC%99%84%EB%B2%BD-%EC%9D%B4%ED%95%B4)
