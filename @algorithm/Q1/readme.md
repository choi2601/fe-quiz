# Q01. What is the time and space complexity of the algorithm?

## ❓ Question

```js
function pow(x, n) {
  if (n === 0) return 1;
  if (n === 1) return x;

  return x * pow(x, n - 1);
}

console.log(pow(2, 4)); // 16
```

- [x] `O(n), O(n)`
- [] `O(n), O(1)`
- [] `O(x^n), O(1)`
- [] `O(x^n), O(n)`

## 🤔 My Thinking

- 시간 복잡도: 함수는 n이 0이 될 때까지 자기 자신을 호출한다. 즉, n에 대해 감소하면서 각 단계마다 한 번의 연산을 수행한다.

- 공간 복잡도: 재귀 함수가 호출될 때마다 현재의 함수 호출은 스택(실행 컨텍스트)에 유지되어야 하므로 n번의 재귀 호출이 스택에 쌓인다.

## 🤓 Answer

Explanation.

The pow function is recursive. There are no problems with calculating the time complexity of a function. The function code will be executed n times, which means the time complexity is O(n).

With the space complexity of recursive functions, things are much more complicated. In addition to the explicitly allocated memory in the function code, we need to take into account the memory spent on storing information about the function call (stack frames) in the call stack.

How long are stack frames stored in memory? Each stack frame is stored in memory until its corresponding function call completes.

The first call to pow (pow(2, 4)) creates a stack frame that stores the parameters x = 2 and n = 4. This call results in another call to pow (pow(2, 3)), which creates a second stack frame , which stores the parameters x = 2 and n = 3. The first call has not yet completed, because the return statement has not yet returned any value. This will continue until the last call is completed. For calling pow(2, 4) we get the following stack:

pow(2, 1)
pow(2, 2)
pow(2, 3)
pow(2, 4)

When n = 1, the function ends with the value x (exit at a certain parameter value is a prerequisite for recurrent functions). Next, stack frames are taken from the stack one by one, starting from pow(2, 1).

Thus, at the same time, a number of stack frames equal to the recursion depth can be stored in memory. That is n in this case.

How much memory does each stack frame take?

The stack frame stores the parameters of the function, its local variables and the return address. In this case, there are no local variables, and the memory required to store the parameters and return address for each stack frame is O(1). This means the memory occupied by the entire stack is O(n).

In general, if each function call creates variables that occupy O(m) memory, then storing the entire recursion tree will require O(nm).

Because of the expense of additional memory and the possibility of running out of memory, recursive solutions are recommended to be used with caution. Any recursive solution can be replaced with an iterative one and this can save memory and sometimes even reduce time complexity.

Next time we will look at the iterative implementation of constructing the pow function.

Code: https://github.com/intspirit/javascript-typescript-questions/blob/main/js/algorithms/6.js

https://www.ideserve.co.in/learn/time-and-space-complexity-of-recursive-algorithms
