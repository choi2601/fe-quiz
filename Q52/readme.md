# Q52. What will be the output?

## ❓ Question

```js
function myFunc(a) {
  console.log(a);
}

myFunc`We make ${"IT"} better!`;
```

- [] `we make IT better!`
- [] `We make better!`
- [] `IT`
- [x] `['We make', 'better!']`
- [] `['We make', 'IT', 'better!']`

## 🤔 My Thinking

템플릿 리터럴(Template Literial)은 ES6에서 새롭게 도입된 기능으로 백팁(``)을 사용하여 문자열과 변수를 함께 사용할 수 있어 문자열 처리에 유용한 기능이다.

태그 된 템플릿 리터럴(Tagged Template Literal)은 템플릿 리터럴의 발전된 형태로써, 함수 형태로 사용할 수 있다.

해당 문법은 문자열에서 정적인 값과 동적인 값을 구분 짓을 수 있다.

```js
function transform(staticValue, ...dynamicValue) {
  console.log(staticValue); // ['Hi', 'and I am', '.']
  console.log(dynamicValue); // ['Choi', 29]
}

const userName = "Choi";
const age = 29;

transform`Hi, ${userName} and I am ${age}.`;
```

첫 번째 파라미터에는 정적 값이 저장되고, 나머지 파라미터에는 동적 데이터가 저장되어 있는 모습을 볼 수 있다.

동적 데이터를 보면 age의 값의 타입이 `String` 이 아닌 `Number` 타입으로 유지되는 것을 볼 수 있다.

즉, 태그 된 템플릿 리터럴 문법을 사용하면 타입에 상관 없이 `Function`, `Number`, `Array`, `Object` 등을 전달하고 이를 실행할 수 있게 된다.

실제 `styled-components` 라이브러리는 태그 된 템플릿 리터럴 문법을 다음과 같이 사용하고 있다.

```js
const Button = styled.a`
  display: inline-block;
  border-radius: 3px;

  ${(props) =>
    props.primary &&
    css`
      background-color: white;
      color: black;
    `}
`;
```

## 🤓 Answer

Explanation.

Tags allow you to parse template literals with a function.

The first argument of a tag function contains an array of string values.
The remaining arguments are related to the expressions.

function myFunc(str, value) {
console.log(str); // ['We make ', ' better!']
console.log(value); // 'IT'

let res = `${str[0]}${value}${str[1]}`;
if (value === 'IT') {
res += ` We are web developers!`;
}

return res;
}

console.log(myFunc`We make ${'IT'} better!`); // We make IT better! We are web developers!

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
