# Q56. What will be the output?

## ❓ Question

```js
const nums = [3, 2, 1, 0];

const data = JSON.stringify(nums, ["0"]);

console.log(data);
```

- [x] `[3, 2, 1, 0]`
- [] `[3]`
- [] `[0]`
- [] `[]`
- [] `Error`

## 🤔 My Thinking

`Replacer` 파라미터는 JSON 문자열에 포함시킬 객체의 속성들을 선택하기 위한 옵션이다.

`Replacer` 파라미터의 값이 `null`로 지정되거나 생략되면, Value 파리미터에 전달한 객체의 모든 속성이 JSON 문자열에 포함된다.

속성의 이름을 배열(Array)의 형태로 전달하면, 해당 속성들만 JSON 문자열에 포함된다.

```js
const products = {
  monitor: { Company: "DELL", Release: 2019 },
  speaker: { Company: "Sony", Release: 2008 },
  radio: { Company: "Aiwa", Release: 1990 },
};

const selected = JSON.stringify(products, ["monitor"]);
//  "monitor: {}"
```

그러나 위 예시와 같이 배열 값과 함께 배열 replacer를 사용하는 경우엔 어떠한 것도 수행되지 않으며 결과값은 동일하다.

## 🤓 Answer

Explanation.

The JSON.stringify() method converts a JavaScript value to a JSON string.

JSON.stringify(value, replacer, space)

The replacer parameter doesn't work as you would expect on array values.
Using an array replacer with an array value won't do anything. The output remains the same.

## 📄 Reference

> https://dillionmegida.com/p/second-argument-in-json-stringify/
