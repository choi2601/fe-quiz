# Q40. What will be the output?

## ❓ Question

```js
function Foo() {
  this.value = 1;
}

function Bar() {
  this.value = 2;
  Foo.call(this);
}

console.log(new Bar());
```

- [] {}
- [] { value: 1 }
- [] { value: 2 }
- [] Error

## 🤔 My Thinking

Bar 함수는 `new` 연산자와 함께 호출됨으로써, this 바인딩은 자신이 생성할 인스턴스인 Bar 참조하게 될 것이다.

해당 상태에서 call 메서드와 함께 Foo 함수를 간접 호출할 경우 명시적으로 this를 지정해주었기 때문에 Foo의 value가 아닌 Bar의 value가 출력될 것이다.

## 🤓 Answer

Explanation.

The call() method calls the function with a given this value and arguments provided individually.

The call (or apply) method can be used to override a constructor:

When we call Foo.call(this) from within the Bar constructor function, the Foo function is called with this referring to the Bar instance and thus overriding its properties.

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call
