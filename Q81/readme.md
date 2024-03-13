# Q81. What will be the output?

## ❓ Question

```js
const obj = {};

obj.foo = function () {
  console.log(bar);
};

obj.__proto__.bar = "baz";

obj.foo();
```

- [x] `baz`
- [] `undefined`
- [] `Error`

## 🤔 My Thinking

모든 객체는 `__proto` 접근자 프로퍼티를 통해 자신의 프로토타입, 즉 `[[Prototype]]` 내부 슬롯에 간접적으로 접근할 수 있다.

`Object.prototype`의 접근자 프로퍼티인 **proto**는 getter/setter 함수라고 부르는 접근자 함수([[Get]], [[Set]] 프로퍼티 어트리뷰트에 할당된 함수)를 통해 [[Prototype]]

내부 슬롯의 값, 즉 프로토타입을 취득하거나 할당한다.

모든 객체는 프로토타입의 계층 구조인 프로토타입 체인에 묶여 있다. 자바스크립트 엔진은 객체의 프로퍼티(메서드 포함)에 접근하려고 할 때, 해당 객체에 접근할려는 프로퍼티가 없다면

**proto** 접근자 프로퍼티가 가리키는 참조를 따라 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다.

프로토타입 체인의 종점, 즉 프로토타입 체인의 최상위 객체는 Object.prototype이며, 이 객체의 프로퍼티와 메서드는 모든 객체에 상속된다.

[[Protoype]] 내부 슬롯의 값, 즉 프로토타입에 접근하기 위해 접근자 프로퍼티를 사용하는 이유는 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해서이다.

```js
const parent = {};
const child = {};

child.__proto__ = parent;
parent.__proto__ = child; // TypeError: Cyclic __proto__ value
```

순환 참조가 되지 않도록 단방향 링크드 리스트를 구현하여야 한다.
