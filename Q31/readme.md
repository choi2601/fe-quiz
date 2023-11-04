# Q31. Which loop will execute faster?

## ❓ Question

```js
class X {
    num = 25;
    foo() {
        return this.num * this.num;
    }
}
console.time('first');
for(let i = 0; i < 1_000_000; i++) {
    new X();
}
console.timeEnd('first');

function Y() {
    this.num = 25;
}
Y.prototype.foo = function() {
    return this.num * this.num;
}
console.time('second');
for(let i = 0; i < 1_000_000; i++) {
    new Y();
}
console.timeEnd('second');
```

- [] first
- [] second
- [x] same time

## 🤔 My Thinking

JavaScript의 `class` 문법은 ES6에 도입되었고, 기존의 프로토타입 기반 상속을 좀 더 명확하고 쉽게 사용할 수 있는 만드는 **syntactic sugar**이다. <br />
즉, class 문법이 기존의 프로토타입을 대체하는 것이 아니라, 내부적으로 프로토타입 체인을 통해 상속 메커니즘을 구현하였다는 점에서 위 두 반복문은 비슷한 성능 효과를 보일 것이다.

## 🤓 Answer

Explanation.

**First of all, despite the fact that the classes are built on top of their counterparts, it cannot be said that they are absolutely the same thing.** See the differences in the MDN article.

Performance also varies.

**On average, across runtime environments, the performance of classes is worse than that of prototypes.**

**In v8 before version 9.7 there was simply a terrible performance in creating an instance of a class that has fields.** The reason for this is a very expensive call to native functions at runtime when initializing a property on a class instance (which is not the case when creating a property on an object literal).

The performance of the class is worse than the prototypes in this case by more than 50 times!

node v17.8 (V8 v9.6)
first: 102.46ms
second: 2.123ms

Starting from version v8 9.7, optimizations were made, thanks to which the performance became almost the same.

Chrome v118 (V8 v11.8)
first: 2.06 ms
second: 1.88 ms

Optimization uses Inline Cache and the need to call a native function disappears in almost 100% of cases. You can read more here.

Results in other browsers:

Safari
first: 50.074ms
second: 23.890ms

Firefox
first: 15ms
second: 9ms