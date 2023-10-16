# Q24. What will be the output?

## ❓ Question

```js
function Counter() {
  this.value = 0;
}

const counter = Counter();
console.log(counter.value++);
```

- [] 0
- [] 1
- [] NaN
- [x] Error

## 🤔 My Thinking

자바스크립트에선 자바와 같은 클래스 기반 객체지향 언어의 생성자과는 다르게 그 형식이 정해져 있지 않고 일반 함수와 동일한 방법으로 생성자 함수를 정의한다. <br />
`new` 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다. 만약 new 연산자와 함께 생성자 함수를 호출하지 않으면 생성자 함수가 아니라 일반 함수로 동작한다. <br />
일반 함수에서의 this는 전역 객체를 가리키며 해당 코드엔 `use strict`가 설정되어 있지 않기 때문에 운영 환경 별 전역 객체가 바인딩 된다. <br />
일반 함수로서 호출된 Counter()의 반환값은 `undefined` 이므로 타입 에러가 발생하게 될 것이다.

## 🤓 Answer

Explanation.

console.log(Counter().value++);
// TypeError: Cannot read properties of undefined (reading 'value')

The Counter function does not return any value. To fix the bug the function must be called as a constructor. When called with new, the function returns this:

const counter = new Counter();
console.log(counter.value++); // 0

If you want users to be able to call your constructor function without new, you can change the function code like this:

function Counter() {
if (!(this instanceof Counter)) {
return new Counter();
}

this.value = 0;
}
