# Q51. What will be the output?

## ❓ Question

```js
const obj = {};

console.log("prop" in obj === obj.hasOwnProperty("prop"));
console.log("toString" in obj === obj.hasOwnProperty("toString"));
```

- [] `true true`
- [x] `true false`
- [] `false true`
- [] `false true`
- [] `false false`

## 🤔 My Thinking

- `in` 연산자는 지정된 속성이 객체 자체 또는 객체의 프로토타입 체인(모든 프로토타입 프로퍼티) 어딘가에 존재하는지를 확인한다
- `hasOwnProperty` 메서드는 속성이 해당 객체 자체에 직접 존재하는지만을 확인한다.

props는 obj 객체나 그 프로토타입 체인에 존재하지 않는다. 반면에 `toString` 은 `Object.prototype` 에 정의되어 있다.

obj는 Object.prototype를 상속받기 떄문에 toString 메서드를 상속 받고 있지만, 그 자체엔 없기 때문에 두 연산식의 실행 결과가 다를 것이다.

프로토타입 체인은 자바스크립트가 객체지향 프로그래밍의 상속을 구현하는 메커니즘이다.

자바스크립트는 객체의 프로퍼티(메서드 포함)에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 `[[Prototype]]` 내부 슬롯의 참조를 따라

자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 탐색한다.

## 🤓 Answer

Explanation.

As the name implies, the method hasOwnProperty() returns only the object's own properties.

The object obj does not have a prop property. Also, the toString property of an object is not its own, but inherited. Therefore, in both cases the hasOwnProperty() method will return false.

On the other hand, the in operator returns true if the property is defined on the object itself or in the prototype chain.

'prop' in obj // false
'toString' in obj // true

console.log('prop' in obj === obj.hasOwnProperty('prop')); // true
console.log('toString' in obj === obj.hasOwnProperty('toString')); // false
