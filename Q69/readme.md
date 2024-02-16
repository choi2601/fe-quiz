# Q69. What will be the output?

## ❓ Question

```js
function foo(i) {
  if (i > 1) {
    return [i];
  }

  return [...foo(i + 1), ...foo(i + 2)];
}

console.log(foo(0));
```

- [] `2`
- [] `2, 3`
- [x] `2, 3, 2`
- [] `2, 3, 2, 3`

## 🤔 My Thinking

foo는 재귀적으로 자기 자신을 호출하며, 특정 조건인 i가 1보다 클 경우 배열에 i값을 포함하여 반환한다.

그렇지 않을 경우 i에 1과 2를 각각 더한 값으로 자기 자신을 두 번 호출하고, 그 결과를 합쳐서 반환한다.

이러한 모든 결과를 모두 합칠 경우 `foo(0)`의 결과는 `[2, 3, 2]`가 된다.

## 🤓 Answer

Explanation.

Recursion is a method of solving a computational problem where the solution depends on solutions to smaller instances of the same problem.

In our example, the foo() function will be called as follows:

foo(0) -> [...foo(1), ...foo(2)]
foo(1) -> [...foo(2), ...foo(3)]
foo(2) -> [2]
foo(3) -> [3]
foo(2) -> [2]

Result: [2, 3, 2]

The order of calls is most clearly visible in the figure. The numbers on the edges of the graph indicate the order of calls.

https://en.wikipedia.org/wiki/Recursion_(computer_science)

Recursion problems for self-training:

[easy] https://leetcode.com/problems/power-of-three/
[medium] https://leetcode.com/problems/powx-n/description/
