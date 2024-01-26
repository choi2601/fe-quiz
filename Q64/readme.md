# Q64. What will be the output?

## ❓ Question

```js
const obj = {
  bar: 100,
  a: () => this.bar,
  foo: function () {
    return () => this.bar;
  },
};

const foo = obj.foo;
const bar = foo();

console.log(bar.call({ bar: 500 }));
```

- [] `100`
- [] `500`
- [] `undefined`
- [] `Error`

## 🤔 My Thinking

1. obj 객체 내의 a 메서드:

`a: () => this.bar`는 화살표 함수이다 화살표 함수는 자신이 선언된 시점의 this 컨텍스트를 유지합니다. 이 경우, a는 객체 리터럴 내에서 선언되었지만, 객체 리터럴은 this 바인딩을 생성하지 않는다.
따라서 a 내의 this는 obj를 가리키지 않고, 그보다 상위 컨텍스트인 전역 this를 가리킨다. 만약 전역 스코프에서 bar가 정의되어 있지 않다면, `a()`는 `undefined`를 반환할 것이다.

2. obj 객체 내의 foo 메서드:

`foo: function () { return () => this.bar; }` 는 일반 함수로 선언되어 있다다 일반 함수는 자신이 호출될 때의 this 컨텍스트를 가진다. 여기서 foo가 obj.foo로
호출되었다면, this는 obj를 가리킬 것이다. 그러나 foo가 `const foo = obj.foo;`로 할당되고, 그 후에 foo()로 호출되었기 때문에, this는 전역 객체를 가리키게 된다. foo() 내부에서 반환되는 화살표 함수는 foo 함수의 this를 유지한다.

3. foo()의 결과인 bar 함수 호출:

`const bar = foo();`는 foo 함수를 호출한다. foo는 화살표 함수를 반환한다. 이 화살표 함수는 foo 함수의 this를 유지하므로, 전역 객체의 bar 속성을 참조합한다.
`bar.call({ bar: 500 })`은 bar 함수에 .call() 메서드를 사용해 새로운 this 컨텍스트 { bar: 500 }를 제공한다. 하지만 화살표 함수는 `.call(), .apply(), .bind()` 메서드로 this 컨텍스트를 변경할 수 없다. 따라서 bar 함수는 원래의 this 컨텍스트, 즉 전역 객체의 bar 속성을 참조한다.
결론적으로, 이 코드의 결과는 전역 객체의 bar 속성 값에 달려 있다. 만약 전역 스코프에 bar 속성이 정의되어 있지 않다면, undefined가 출력된다. 그렇지 않고 전역 스코프에 bar가 정의되어 있으면, 해당 값이 출력된다.

이 코드는 전역 bar의 값을 직접 설정하지 않았으므로, undefined가 가장 가능성 있는 출력 결과이다.

## 🤓 Answer

Explanation.

Because we do not call the foo() function as a method of an object (const bar = foo()) and also did not bind the context value manually, for example, using the bind() or call() method, then this inside the foo() function refers to the global object.
In strict mode, this will be undefined in this case.

The this value inside an arrow function is inherited from the parent when the function is created and is never changed. The context passed to the arrow function using the call() method will be ignored.

Because the context of the parent function is a global object, the context of the arrow function is also a global object.

There is no bar variable in the global object, so this.bar inside the arrow function is undefined.
