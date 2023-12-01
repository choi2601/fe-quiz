# Q48. What will be the output?

## ❓ Question

```js
const numbers = ["9", "10", "11"].map(parseInt);

console.log(numbers);
```

- [] `[9, 10, 11]`
- [] `[NaN, NaN, NaN]`
- [] `[NaN, 2, 3]`
- [x] `[9, NaN, 3]`

## 🤔 My Thinking

`map` 함수는 배열의 각 요소에 대해 주어진 함수를 호출한다. 이때 각 요소에 대해 호출되는 함수에 두 개의 인자를 전달하는데, 현재 요소와 그 요소의 인덱스이다.

마찬가지로 `parseIn` 또한 두 개의 인자를 받을 수 있다. 파싱할 문자열과 진법(radix)을 지정할 수 있으면 문자열의 내용에 따라 기수를 추측한다.

따라서 `['9', '10', '11']`은 다음과 같이 호출된다.

- `parseInt('9', 0)`: 인덱스 0은 10진수로 간주되므로 결과는 9이다.
- `parseInt('10', 1)`: 1진수는 존재하지 않으므로 결과 NaN이다.
- `parseInt('11', 2)`: 2진수에서 11은 3으로 해석된다.

## 🤓 Answer

Explanation.

The map method passes two parameters to the callback - the value and index of the current element.

The parseInt function also takes two parameters - the string to convert to a number and the radix of the numeric string.

A valid radix value is an integer in the range between 2 and 36.

If radix is ​​not specified or is 0, then javascript assumes the following:

If the input string starts with "0x", then radix = 16. In any other case, radix = 10

So in the original example:

parseInt('9', 0) -> radix = 10 -> result = 9
parseInt('10', 1) -> radix = 1 -> result = NaN
parseInt('11', 2) -> radix = 2 -> result = 3

To avoid errors, always specify radix explicitly.
