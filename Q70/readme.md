# Q70. What will be the output?

## ❓ Question

```js
"use strict";

Object.defineProperty(Object.prototype, "foo", {
  writable: false,
  value: 1,
});

const bar = { foo: 123 };

const clone1 = { ...bar };

console.log(clone1.foo);

const clone2 = Object.assign({}, bar);

console.log(clone2.foo);
```

- [] `123, 123`
- [x] `123, Error`
- [] `1, 1`
- [] `1, Error`
- [] `Error`

## 🤔 My Thinking

JavaScript에서는 속성을 추가하거나 복제하는 방식에 따라, 읽기 전용 속성에 대한 처리가 다르며, 이는 객체 리터럴을 통해 정의하거나

스프레드 연산자를 사용할 때와 `Object.assign` 메서드를 사용할 때의 차이점으로 확인할 수 있다.

- 직접 할당을 시도한 경우: 만약 엄격 모드(`use strict`)에서 어떤 객체의 `foo`속성에 값을 할당하려고 하면, foo가 읽기 전용이기 때문에,
  JavaScript 엔진은 `TypeError` 오류를 발생시킨다.

- 객체 리터럴을 통한 속성 정의: 객체 리터럴을 사용하여 객체를 생성하고 속성을 정의할 때는, 속성을 **정의** 한다. 즉 객체가 처음 생성될 때 `foo`를
  포함시키므로, 이 경우에는 읽기 전용 속성에도 불구하고 성공적으로 새로운 값을 할당할 수 있다. <br /> 프로토타입의 프로퍼티와 값은 이름의 인스턴스에 추가하면 프로토타입 체인을
  따라 프로토타입 프로퍼티를 검색하여 프로토타입 프로퍼티를 덮어쓰는 것이 아니라 인스턴스 프로퍼티로 추가한다. <br /> 이처럼 상속 관계에 의해 프로퍼티가 가려지는 현상을 프로퍼티 섀도잉(property shadowing)이라 한다.
- 객체 복제 방식의 차이
  - 스프레드 연산: 스프레드 연산자는 속성을 정의하는 방식을 사용하기 때문에 읽기 전용 속성이 있어도 복제 과정에서 오류가 발생하지 않는다.
  - Object.assign: Object.assign 방식은 속성을 할당하는 방식을 사용한다. 이 경우, 프로토타입 체인에서 foo 속성을 찾고, 그 속성의 디스크립터(읽기 전용)을 사용하여 새 값을 할당하려고 한다. 하지만 이는 읽기 전용이기 때문에 `TypeError` 오류가 발생한다.

## 🤓 Answer

Explanation.

Object.defineProperty(Object.prototype, 'foo', {
writable: false,
value: 1,
});

This piece of code sets the read-only property foo that is inherited by all objects.
As a result we can’t use assignment syntax to create the own property foo anymore

const baz = {};
baz.foo = 2;

In strict mode we will get an error TypeError: Cannot assign to read only property 'foo'.

But we still may create the property foo via an object literal:

const bar = { foo: 2 };

since object literals don’t set properties, they define them:

const bar = {};
Object.defineProperty(bar, 'foo', {
writable: true,
value: 2
});

The main difference between object assigning and object defenition that the main purpose of assignment is making changes, and the main purpose of definition is to create an own property.

That's why the assigning algorithm, as opposed to the defenition algorithm, is looking for the property in the prototype chain and if founded uses its descriptor when assigning new value.

The following example clones an object in two different ways. The spread operator uses the property defenition algorithm in its implementation, so cloning occurs without error.

const clone1 = { ...bar };
console.log(clone1.foo); // 123

The Object.assign method uses assignment syntax to create properties, so its use results in an error.

const clone2 = Object.assign({}, bar); // TypeError: Cannot assign to read only property 'foo' of object '#<Object>'

More detail about object assigning vs object defininion can be found here

https://exploringjs.com/deep-js/ch_property-assignment-vs-definition.html
