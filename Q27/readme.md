# Q27. What will be the output?

## ❓ Question

```js
console.log(isFinite(null), isFinite(undefined), isFinite(NaN), isFinite(2e64));
```

- [] true true true true
- [] true true true false
- [] true true false true
- [x] true false false true
- [] false false false false

## 🤔 My Thinking

`isFinite`는 주어진 값이 유한한 숫자(finite number)인지 확인한다. <br />
null 지체는 값이 없음을 의미한다. 하지만 수학적 연산이나 다른 타입과의 비교에서는 0으로 취급된다. <br />
undefined는 숫자로 변환되면 NaN(Not a Number)이되고, 2e64는 그 값이 매우 큰 숫자이지만, 처리할 수 있는 유한수 범위 내에 있다.

## 🤓 Answer

Explanation.

The isFinite() function determines whether the passed value is a finite number.
The function returns false if the argument is coerced to Infinity or NaN or undefined. Otherwise, true.

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isFinite

> JavaScript는 원래 웹 페이지를 동적으로 만들기 위해 개발되었고, 쉽게 사용할 수 있어야 했습니다. 동적 타이핑과 자동 형변환은 이러한 목표를 지원합니다. <br /> 개발자가 명시적으로 데이터 타입을 관리할 필요가 없으므로, 빠르게 프로토타이핑을 할 수 있습니다. <br /> **개발 속도**: 명시적인 타입 선언 없이도 변수를 생성하고 조작할 수 있기 때문에 개발 속도가 빨라집니다. <br /> **유연성**: 동적 타이핑은 코드가 더 유연해지게 해줍니다. 같은 변수에 다른 타입의 값을 할당할 수 있으므로, 다양한 상황에서 쉽게 사용할 수 있습니다. <br /> **간결성**: 타입을 명시하지 않아도 되므로 코드가 더 간결해집니다. <br /> 그러나 이런 유연성은 신중하게 다루어야 합니다. 자동 형변환이 예상치 못한 결과를 가져올 수 있으므로, 복잡한 애플리케이션에서는 종종 문제가 될 수 있습니다. 이러한 문제를 해결하기 위해 TypeScript와 같은 정적 타이핑이 도입된 언어 확장도 있습니다.
