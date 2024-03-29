# Q86. What will be the output?

## ❓ Question

```js
globalThis.name = "foo";

function log(name) {
  new Function("\tconsole.log(name);")();
}

log("bar");
```

- [x] `foo`
- [] `bar`
- [] `undefined`
- [] `Error`

## 🤔 My Thinking

Function 생성자로 만들어지는 함수는 실행 컨텍스트에 대한 클로저(closure)를 생성하지 않는다.

함수 생성자는 항상 전역 범위에서 생성이 된다. 함수가 실행될 때, 자신의 지역 변수와 전역 변수에만 접근할 수 있으며

Function 생성자가 호출된 그 범위의 변수에는 접근할 수 없기 때문에 전역 객체의 name인 foo가 출력된다.

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function
