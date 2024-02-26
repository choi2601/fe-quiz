# Q75. What will be the output?

## ❓ Question

```js
const authorizedUsers = new Map();
const authorizedUsersWeak = new WeakMap();

function login(user) {
  authorizedUsers.set(user, true);
  authorizedUsersWeak.set(user, true);
}

let john = { id: 1, name: "John" };

login(john);

john = null;

console.log(authorizedUsers.size, authorizedUsersWeak.size);
```

- [] `1 1`
- [] `1 0`
- [x] `1 undefined`
- [] `0 0`
- [] `Error`

## 🤔 My Thinking

`Map` 객체는 키와 값을 연결하며 키에 대한 참조를 강력하게 유지한다. 반면, `WeakMap`은 객체 또는 등록되지 안흔 심볼만을 키로 허용하며, 키에 대한 참조를 약하게 유지한다.

이는 `WeakMap`의 키로 사용된 객체가 다른 곳에서 참조되지 않게 되면, 가비지 컬렉션의 대상이 될 수 있음을 의미한다.

1. john 객체를 생성하고 login 함수를 통해 authorizedUsers Map과 authorizedUsersWeak WeakMap에 john 객체를 키로 하여 추가한다.
2. 이후 john 변수에 null을 할당하여, john 객체에 대한 강력한 참조를 제거한다. 이 시점에서 authorizedUsers Map은 여전히 john 객체에 대한 참조를 유지하지만, authorizedUsersWeak WeakMap에서는 john 객체가 가비지 컬렉션의 대상이 될 수 있다.

authorizedUsers.size는 1을 출력한다. Map은 john 객체에 대한 참조를 강력하게 유지하고 있기 때문에, 크기가 1인 상태를 유지한다.

authorizedUsersWeak.size에 대한 접근은 undefined를 결과를 낳는다. WeakMap은 .size 프로퍼티를 제공하지 않으며, 그 크기를 직접 확인할 수 없다. WeakMap의 키가 되는 객체가 가비지 컬렉션에 의해 언제 수집될지 알 수 없으며, 이 때문에 WeakMap의 크기를 직접적으로 확인하는 방법은 제공되지 않는다.

_강력한 참조_ 란 프로그래밍 언어에서 어떤 객체에 대한 참조가 가비 컬렉션(GC)의 대상이 되지 않도록 보호하는 참조를 의미한다.

즉, 객체에 대한 강력한 참조가 있으면 해당 객체는 메모리에서 자동으로 해제되지 않는다. 이는 해당 객체가 여전히 필요하고 사용 중임을 의미한다.

강력한 참조는 변수, 객체의 속성, 배열 등 다양한 방식으로 객체를 참조할 수 있다.

강력한 참조는 메모리 누수를 일으킬 수 있는 원인 중 하나이다. 객체가 더 이상 필요하지 않음에도 불구하고 어딘가에서 계속 참조되고 있다면, 그 객체는 메모리에서

해제되지 않아 필요 없는 메모리를 계속 차지하게 된다.

## 🤓 Answer

Explanation.

A WeakMap is a collection of key/value pairs whose keys must be objects (or symbols), and which does not create strong references to its keys. That is, an object's presence as a key in a WeakMap does not prevent the object from being garbage collected. Once an object used as a key has been collected, its corresponding values in any WeakMap become candidates for garbage collection as well — as long as they aren't strongly referred to elsewhere.

A WeakMap doesn't allow observing the liveness of its keys, its keys are not enumerable.
There is no method to obtain a list of the keys. If there were, the list would depend on the state of garbage collection, introducing non-determinism. If you want to have a list of keys, you should use a Map.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap
