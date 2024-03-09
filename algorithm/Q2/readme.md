# Q02. What is the time and space complexity of the algorithm?

## ❓ Question

```js
function pow(x, n) {
  let res = 1;

  for (let i = 0; i < n; i++) {
    res *= x;
  }

  console.log(pow(2, 4));
}
```

- [] `O(n), O(n)`
- [x] `O(n), O(1)`
- [] `O(x^n), O(1)`
- [] `O(x^n), O(n)`

## 🤔 My Thinking

- 시간 복잡도: `for` 루프는 n번 반복되어, n에 비례하여 증가한다.

- 공간 복잡도: 변수 `res`와 `i`만을 사용하며, 실행 시간동안 고정된 크기의 공간을 차지한다. n의 값이 커져도 추가적인 공간이 필요하지 않는다.

## 🤓 Answer

Explanation.

As was said in the last quiz, any recursive solution can be replaced with an iterative one. This is exactly what we did with the pow() function. Sometimes this solution loses in readability, but often wins in memory, and even time complexity.

In this case, the time complexity is also O(n), since n iterations are required to calculate the result. But space complexity has decreased. Now we don’t need additional memory to store all the stack frames; instead, for the function to work, we only need memory to store the variables x, n, res and i. Despite the fact that the variable i is created every iteration (
because we used the let keyword to create it), it will require O(1) memory, since its lifetime is one iteration.

Algorithm time complexity O(n), space complexity O(1).

Do you think it is possible to create an algorithm for the pow() function with less time complexity?

https://www.baeldung.com/cs/convert-recursion-to-iteration
