# Q60. What will be the output?

## ❓ Question

```js
function argsToString(...args) {
  const foo = args.join(",");
  const bar = arguments.join(",");
  return foo === bar;
}

console.log(argsToString(1, 2, 3));
```

- [] `true`
- [] `false`
- [x] `Error`

## 🤔 My Thinking

자바스크립트의 `arguments` 객체는 모든 함수 내에서 이용 가능한 지역 변수이다.
`arguments` 객체를 사용하여 함수 내에서 모든 인수를 참조할 수 있으며, 호출할 때 제공한 인수 각각에 대한 항목을 갖고 있다.

```js
arguments[0];
arguments[1];

arguments[1] = "new value";
```

**`arguments` 객체는 `Array`가 아니다.**
`Array`와 비슷하지만, `length` 빼고는 어떠한 `Array` 속성을 가지지 않는다.

즉, `arguments` 객체는 유사 배열 객체(array-like-object)이며, 이터러블(iterable) 객체이다.

`arguments` 객체에서 배열 메서드를 사용하려면 아래와 같이 사용할 수 있다.

```js
var args = Array.prototype.slice.call(arguments);
var args = [].slice.call(arguments);

var args = Array.from(arguments);
var args = [...arguments];
```

## 🤓 Answer

Explanation.

The rest operator collects all the arguments in an array.
Next, the join method turns the elements of the array into a string, as expected.

```js
const foo = args.join(","); // 1,2,3
```

Next, the join method is also applied to the arguments.

```js
const bar = arguments.join(",");
```

However, this line will throw an error because arguments is not an array, but an array-like object on which the join method is not defined.

_TypeError: arguments.join is not a function_

To fix the error, we can either borrow the array's join method

```js
const bar = [].join.call(arguments, ","); // 1,2,3
```

or use the spread operator to turn arguments into an array (we can do this because arguments is an iterable object)

```js
const bar = [...arguments].join(","); // 1,2,3
```

or use the Array.from() method

```js
const bar = Array.from(arguments).join(","); // 1,2,3
```
