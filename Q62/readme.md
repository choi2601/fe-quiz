# Q62. What will be the output?

## ❓ Question

```js
let num = "10";
let res;

switch (num) {
  case "10":
    res = "10";
  case 10:
    res = 10;
}

console.log(typeof res);
```

- [] `string`
- [x] `number`
- [] `undefined`
- [] `Error`

## 🤔 My Thinking

`break`나 `return`문이 없기 때문에 첫 번째 블록의 코드를 실행한 후에 switch 루프의 실행을 종료하는 대신에 이후의 모든 case들이 실행이 된다.

그래서 기대되는 타입 값인 `string`이 아닌 `number` 타입 결과가 나온다.

## 🤓 Answer

Explanation.

The problem with this quiz is not with type casting, but with the lack of break statements inside case blocks.

The conditions of case blocks are strictly checked, however, due to the absence of a break in the first case, after executing the code in the first block, instead of ending the execution of the switch loop, the engine will execute all subsequent case blocks until a break or return statement is encountered or until the blocks will not end.

To fix:

```js
switch (num) {
  case "10":
    res = "10";
    break;
  case 10:
    res = 10;
    break;
}

console.log(typeof res); // string
```

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch
