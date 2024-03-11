# Q79. What will be the output?

## ❓ Question

```html
<script>
  const foo = 1;
  var bar = 2;
</script>
<script>
  console.log(foo, bar);
</script>
```

- [] `1, 2`
- [] `undefined, 2`
- [] `undefined, undefined`
- [] `Error`

## 🤔 My Thinking

- `const` 키워드로 선언된 foo는 블록 스코프를 가진다. `<script>` 태그 내부에서 선언되어 있기 때문에 전역 컨텍스트에서도 접근 가능하다.
- `var` 키워드로 선언된 bar는 함수 스코프를 가진다. 그러나 이 경우에도 `<script>` 태그 내부에서 전역 컨텍스트로 선언되므로 전역 변수처럼 동작한다.

웹 페이지에서 `<script>` 태그를 사용하여 JavaScript 코드를 작성하면, 그 안에서 선언된 변수는 기본적으로 전역 스코프(global scope)에 속하게 된다.

이는 `<script>` 태그 내부에 선언된 변수들이 별도의 함수 또는 블록 내에 있지 않는 한, 웹 페이지의 전역 실행 컨텍스트(global execution context)에 선언되기 때문이다.

`var`로 선언된 전역 변수는 `window` 객체의 속성이 되지만 `let`이나 `const`로 선언된 전역 변수는 별도의 메모리 공간에 저장이 된다.

## 🤓 Answer

Explanation.

Arrow functions don't have their own this. Instead this inside an arrow function's body points to the this value into the scope the arrow function is defined within.

Our function is defined in the global scope.

this in global scope refer to the global object (even in strict mode).
