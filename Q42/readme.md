# Q42. What will be the output?

## ❓ Question

```js
const map = new Map([{ name: "Alex" }, { name: "John" }]);

console.log([...map.values()]);
```

- [] `[{name: 'Alex'}, {name: 'John'}]`
- [] `['Alex', 'John']`
- [] `[{name: 'Jogn'}]`
- [x] `[undefined]`
- [x] `Error`

## 🤔 My Thinking

`new Map([{ name: 'Alex' }, { name: 'John' }])`은 올바른 Map 생성 방식이 아니다.

Map 객체를 생성할 때는 키-값 쌍의 배열을 전달해야 한다. 예를 들어 위 코드의 올바른 이터러블은 아래와 같을 것이다.

```js
const map = new Map([
  ["name", "Alex"],
  ["name", "John"],
]);

// ['John']
console.log([...map.values()]);
```

## 🤓 Answer

Explanation.

The Map() constructor creates Map objects.

new Map(iterable)

where iterable is an Array or other iterable object whose elements are key-value pairs.
(For example, arrays with two elements, such as [[1, 'one' ],[ 2, 'two']].)
Each key-value pair is added to the new Map.

The values() method returns a new map iterator object that contains the values for each element in the Map object.

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/Map
