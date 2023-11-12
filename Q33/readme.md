# Q33. What will be the output?

## ❓ Question

```js
function* generatorFunction() {
  return "Let's make IT better!";
}

console.log(typeof generatorFunction());
```

- [] string
- [x] object
- [] generator
- [] Error

## 🤔 My Thinking

`generatorFunction` 은 제너레이터 함수이다. 제너레이터 함수를 호출하면 제너레이터 객체가 반환된다.
해당 객체는 `next()`, `return()`, `throw()`와 같은 특정 메서드를 가진 이터러블(iterable)이며,
`object` 타입에 속한다.

위 함수에서 최종적으로 return을 사용하였으니, 아래와 같이 제너레이터 객체를 종료시키고 제공된 값을 반환할 것이다.

```js
{ value: 'Let\'s make IT better!', done: true };
```

## 🤓 Answer

Explanation.

**Whereas a regular function returns whatever comes after the return statement (or undefined if there is no return), a generator returns a special Generator object.**

console.log(generatorFunction()); // generatorFunction {<suspended>}
console.log(typeof generatorFunction()); // object

The Generator object is an iterator - an object with a next() method that is used to iterate through values.

Initially the generator is in the suspended state.

By calling the next() method we get the value produced by the generator using a yield or return statement.

generator.next(); // { value: "Let's make IT better!", done: true }

The return call terminates the generator, it changes its status from suspended to closed and the value of the done property becomes true.

console.log(generatorFunction()); // generatorFunction {<closed>}
generator.next(); // { value: undefined, done: true }

Another case of closing a generator is when there are no more yield statements.
