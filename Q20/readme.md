# Q20. Which function will execute faster?

## ❓ Question

```js
function createArr() {
  const arr = new Array(10_000_000);
  for (let i = 0; i < 10_000_000; i++) {
    arr[i] = Math.random();
  }
  return arr;
}

function foo() {
  for (let i = 0; i < arr.length; i++) {
    someFunc(arr[i]);
  }
}

function bar() {
  for (let i = 0; arr[i] !== undefined; i++) {
    someFunc(arr[i]);
  }
}

const arr = createArr();
foo();
bar();
```

- [x] foo
- [ ] bar
- [] same time

## 🤔 My Thinking

`arr.length`는 루프가 시작하기 전에 한 번만 계산이 되고 이후 i의 길이가 전체 배열의 길이보다 작은지 확인을 한다. <br />
bar 함수에서 인덱스를 통해 arr 배열에 요소를 접근하는 방식은 매 반복마다 `Math.random`을 통해 생성된 난수에 대해서 undefined와 비교하는 것은 단순 배열의 길이와
인덱스를 비교하는 것보다 다소 비효율적일 수 있다.

## 🤓 Answer

Explanation.

Function execution time on my device:

foo: 11.654ms
bar: 38.895ms

There are two problems with the loop in the bar function:

1. Math.random() returns numbers of type double. **Comparing undefined with a double number is quite expensive**. If you replace the double numbers with integers in the example, the bar() function will show much better performance.

2. In the last iteration we try to get an element arr[i] outside the array. **In this case, the engine will look for this key in the prototype chain. In addition to the fact that this operation itself is expensive, it also causes de-optimization of the array, since the optimized version was not designed for such calls. This makes all further standard array operations slower.**

To see this deoptimization, run the code with special flags:

node --trace-opt --trace-deopt index.js

The output will be something like this:

```
[marking 0x034a7b6429f1 <JSFunction bar (sfi = 0x34a1e749cb1)> for optimized recompilation, reason: small function]
[compiling method 0x034a7b6429f1 <JSFunction bar (sfi = 0x34a1e749cb1)> (target TURBOFAN) using TurboFan OSR]
[optimizing 0x034a7b6429f1 <JSFunction bar (sfi = 0x34a1e749cb1)> (target TURBOFAN) - took 0.007, 1.252, 0.013 ms]
[bailout (kind: deopt-eager, reason: out of bounds): begin. deoptimizing 0x034a7b6429f1 <JSFunction bar (sfi = 0x34a1e749cb1)>, opt id 2, bytecode offset 9, deopt exit 5, FP to SP delta 104, caller SP 0x7ff7b47218e0, pc 0x000110947bf2]
```

The last line is about deoptimization: kind: deopt-eager, reason: out of bounds
