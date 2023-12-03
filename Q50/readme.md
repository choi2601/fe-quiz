# Q50. What will be the output?

## ❓ Question

```js
const str1 = "How\nyou\ndoing";
const str2 = `How
you
doing
`;

console.log(str1 === str2);
```

- [] `true`
- [x] `false`
- [] `Error`

## 🤔 My Thinking

str1은 `\n` 문자로 구분된 하나의 문자열이다. 반면에 str2는 템플릿 리터럴을 통해 문자열을 작성하였고, 각 줄의 끝에는 실제 줄바꿈 문자가 포함된다.

따라서 str2의 문자열 구성은 `How\nyou\ndoing\n`이기 때문에 str1과 다른 문자열로 판별된다.

## 🤓 Answer

Explanation.

Strings are compared by value. The values ​​of these two strings are equal.
The ability to break a line without using a \n is one of the features of backtick character.
