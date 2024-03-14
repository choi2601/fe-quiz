# Q81. What will be the output?

## ❓ Question

```js
const arr = new Array(5).map((i, j) => j);

console.log(arr);
```

- [] `[0, 1, 2, 3, 4, 5]`
- [] `[1, 2, 3, 4, 5]`
- [] `[5]`
- [x] `[<5 empty items>]`

## 🤔 My Thinking

단일 숫자 매개변수가 있는 생성자를 사용하여 배열을 만들 경우, 해당 배열은 `length` 속성이 해당 숫자로 설정되어 생성되며

배열의 요소는 빈 슬롯(empty slot)이다.

`map` 메서드는 배열의 실제 존재하는 요소에 대해서만 함수를 실행한다. 그러므로 empty slot만 있는 배열은 무시된다.

```js
const arrayEmpty = new Array(2);

console.log(arrayEmpty.length); // 2
console.log(arrayEmpty[0]); // undefined이지만, 빈 슬롯
console.log(0 in arrayEmpty); // false
console.log(1 in arrayEmpty); // false
```

## 🤓 Answer

Explanation.

When called with a single argument that is an integer in the range 0 to 2^32 - 1, the Array constructor creates an array of empty slots of the specified length.

Empty slots are not the same as slots filled with the value undefined.

According to MDN, the map callbackFn argument is invoked only for array indexes which have assigned values. It is not invoked for empty slots in sparse arrays. This also applies to other iterative methods, such as forEach.

**However, in some operations, empty slots behave as if they are filled with undefined.**

**One such operation is spreading.**

**And this can be used if, knowing only the number of required elements n, you want to create a sequence of numbers from 0 to n.**

const arr = [...new Array(5)].map((i, j) => j);

console.log(arr); // [0, 1, 2, 3 4]

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Array

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map#description
