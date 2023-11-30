# Q47. What will be the output?

## ❓ Question

```js
function getFruits(...fruitList, favorite) {
    return favorite;
}

console.log(getFruits('apple', 'banana', 'orange'))
```

- [] `orange`
- [] `banana`
- [] `undefined`
- [x] `Error`

## 🤔 My Thinking

Rest 파라미터는 자바스크릡트 ES2015(ES6)부터 처음 도입되었다.

함수의 파라미터에 사용되며, 뒤에 남은 요소들을 배열 형태로 받아 주는 역할을 한다.

그래서 위의 코드와 같이 Rest 파라미터를 앞의 인자에 사용을 한다면 다음과 같은 에러가 발생한다.

> SyntaxError: Rest element must be last element.

## 🤓 Answer

Explanation.

This piece of code will throw an error because the rest parameter can only be the last parameter of the function.

SyntaxError: Rest parameter must be last formal parameter
