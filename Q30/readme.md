# Q30. What will be the output?

## ❓ Question

```js
class Circle {
  static radius = 5;
  static diameter = this.radius * this.radius;
}

console.log(Circle.diameter);
```

- [x] 25
- [] NaN
- [] undefined
- [] Error

## 🤔 My Thinking

정적 속성에서의 this는 클래스 자체를 참조한다. 따라서 `this.radius * this.radius`는 실제로 `Circle.radius * Circle.radius`를 의미하며 이에 대한 결과는 25가 된다.

## 🤓 Answer

Explanation.

The static keyword defines a static method or field for a class.
Static properties cannot be directly accessed on instances of the class.
Instead, they're accessed on the class itself.

In the field initializer, this refers to the current class (which you can also access through its name).

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static
