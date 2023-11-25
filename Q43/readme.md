# Q43. What will be the computed property of a_class?

## ❓ Question

```js
this.a = "outer a";
this.b = "outer b";

class A {
  a = "innerA";
  b = "innerB";
  [this.a] = this.b;
}

const a_class = new A();

console.log(a_class);
```

- [] `{innerA: innerB}`
- [] `{outerA: outerB}`
- [x] `{outerA: innerB}`
- [] `{innerA: outerB}`
- [] `${outerA: undefined}`
- [] `${undefined: innerB}`

## 🤔 My Thinking

계산된 속성 이름 `[this.a] = this.b;`는 클래스의 정의 시점에서의 this 컨텍스트를 참조한다.
클래스 정의 시점에서의 `this`는 클래스 외부의 `this`, 즉 전역 컨텍스트(전역 환경 레코드 내 선언적 환경 레코드\_Declarative Environment Record)를 가리킨다.

클래스 정의 시점에서의 this의 범위와 클래스 인스턴스 내의 this의 범위가 다르기 때문에 `{outerA: innerB}`의 결과값이 나올 것이다.

## 🤓 Answer

Explanation.

When a class declaration is evaluated, its elements property keys are evaluated in the order of declaration. If the property key is computed, the computed expression is evaluated, with the this value is set to the this value surrounding the class (not the class itself).

Property values are evaluated during instance creation with this set to the instance itself.

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes
