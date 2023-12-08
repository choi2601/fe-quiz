# Q53. What will be the output?

## ❓ Question

```js
class Foo {
  x = 1;
  y = this.z;
  z = ++this.x;
}

const foo = new Foo();

console.log(foo.x, foo.y, foo.z);
```

- [] `1, 1, 1`
- [] `1, 1, 2`
- [x] `1, undefined, 2`
- [] `2, 2, 2`
- [] `2, undefined, 2`

## 🤔 My Thinking

클래스의 속성은 선언된 순서대로 초기화된다

1. `x = 1;` 는 x를 1로 초기화한다.
2. `y = this.z;` 는 y에 this.z의 값을 할당한다. 이 시점에서 z는 아직 초기화되지 않았기 때문에 y는 undefined가 된다.
3. `z = ++this.x;` 는 this.x의 값을 1 증가시킨 후(선위 연산자) z에 할당한다. 따라서 x는 2가 되고, z 역시 2가 된다.

## 🤓 Answer

Explanation.

Fields of a class are added one-by-one.
Field initializers can refer to field values above it, but not below it.

The increment operator, if used prefix (++x), increments and returns the value after incrementing.

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Public_class_fields
