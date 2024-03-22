# Q03. Using additional memory to solve the problem best way what data structure will you use?

## ❓ Question

```js
// Given an array of unique numbers, you need to find two numbers
// that add to the given number.

function twoSum(nums: number[], target: number): number[] {}
```

- [] `array`
- [x] `hash table`
- [] `linked list`
- [] `won't use additional memory`

## 🤔 My Thinking

```js
function twoSum(nums: number[], target: number): number[] {
  const numMap = new Map();

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];

    if (numMap.has(complement)) {
      return [numMap.get(complement), i];
    }

    numMap.set(i, nums[i]);
  }

  return [];
}
```

## 🤓 Answer

Explanation.

Let's write down a solution to the problem without using additional memory.

1. Brute force approach. For each element of the array, we will perform another traversal through the array to add the element with each other. If successful, we will return a pair of indexes.

```js
function twoSum(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = 0; j < nums.length; j++) {
      if (i === j) continue; // skip addition of the same element

      if (nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }

  return [];
}
```

Since we have nested loops, in the worst case the complexity of the algorithm will be O(n^2).

Executing all test cases took 172ms.

2. We can improve this solution somewhat by not adding the same elements twice, such as nums[0] + nums[1] and nums[1] + nums[0].

To do this, we will start the inner loop not from 0, but from i + 1.

```js
function twoSum(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }

  return [];
}
```

Executing all test cases took 110ms.

3. Walking through the inner loop we are looking for a specific number whose value will be equal to target - nums[i].

The problem with an array is that to find the required value we need to perform n iterations.

To quickly search by arbitrary key, use the hash table data structure (hash map).

Hash Maps are store data in key-value pairs. Inserting and searching operations are completed in O(1) time on average.

In JavaScript, the implementation of a hash table is the Map structure.

Let's create an additional map variable, where the key is the value and the value is the index of the element.

```js
function twoSum(nums, target) {
  const map = new Map(nums.map((v, i) => [v, i]));

  for (let i = 0; i < nums.length; i++) {
    const diff = target - nums[i];
    const val = map.get(diff);
    if (val !== undefined && i !== val) {
      return [i, val];
    }
  }

  return [];
}
```

We got an algorithm with linear complexity. Executing all test cases took 60ms.
