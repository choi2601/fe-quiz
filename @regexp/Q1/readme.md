# Q01. What will be the output?

## ❓ Question

```js
const reg = /\-/gi;

const match1 = reg.exec("2-1-1");
const match2 = reg.exec("2-1-2");
const match3 = reg.exec("2-1-3");

console.log(match1?.index, match2?.index, match3?.index);
```

- [] `1,1,1`
- [] `3,3,3`
- [] `undefined, undefined, undefined`
- [x] `1,3,undefined`

## 🤔 My Thinking

`/-\/gi` 정규표현식은 문자열에서 모든 대시('-') 문자를 찾는다.

`exec` 메소드는 정규표현식에서 일치하는 첫 번째 결과를 찾은 후, 해당 결과에 대한 정보를 담은 배열을 반환한다.

만약 일치하는 결과가 있다면, 정규표현식 객체의 `lastIndex` 속성을 업데이트하여 다음 `exec` 호출 시 다음 일치 항목부터 검색을 시작한다.

위의 경우 동일한 정규표현식 객체를 사용하여 여러 번 `exec` 메소드를 호출하였기 때문에, 마지막 대시 인덱스(3) 이후엔 검색이 되지 않기 때문에 index의 값은 `undefined`가 출력된다.

## 🤓 Answer

Explanation.

JavaScript RegExp objects are stateful when they have the global or sticky flags set (e.g. /foo/g or /foo/y). They store a lastIndex from the previous match.

The exec() method of RegExp instances executes a search with this regular expression for a match in a specified string and returns a result array, or null.

```js
console.log(match1); // [ '-', index: 1, input: '2-1-1', groups: undefined ]
```

If the match succeeds, the exec() method returns an array and updates the lastIndex property of the regular expression object.

```js
let match1 = reg.exec("2-1-1");
console.log(reg.lastIndex); // 2

let match2 = reg.exec("2-1-2");
console.log(reg.lastIndex); // 4

let match3 = reg.exec("2-1-3");
console.log(reg.lastIndex); // 0
```

The exec() can be used to iterate over multiple matches in a string.

```js
while ((match = reg.exec("2-1-1-4-5"))) {
  console.log(match.index); // 1, 3, 5, 7
}
```

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec
