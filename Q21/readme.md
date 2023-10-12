# Q21. Updating array elements with which indexes produces the worst performance in V8?

## ❓ Question

```js
function createArr() {
  const arr = new Array(10_000_000);

  for (let i = 0; i < 10_000_000; i++) {
    arr[i] = i;
  }

  arr[0] = 0.1;
  arr[1] = 10;
  arr[2] = "10";
  arr[3] = { a: "hello" };

  return arr;
}

const arr = createArr();
```

- [ ] 0, 1
- [ ] 2, 3
- [x] 0, 2
- [] 1, 3
- [] same times

## 🤔 My Thinking

배열 arr는 처음에는 정수로 채워지며 V8 엔진은 배열의 원소들이 모두 같은 타입일 때 해당 배열을 최적화한다.
위 예시의 해당 배열에 대해 일부 인덱스의 값을 변경하면서 타입을 혼합할 경우 최적화가 깨지게 된다. <br>

인덱스 0에는 0.1이라는 소수를 저장하여 원래의 정수 배열이 실수를 포함하게 되고 이후 인덱스 2에는 "10"이라는 문자열을 저장한다. <br />
이렇게 되면 V8 엔진은 배열이 더 이상 순수한 정수 배열이 아니라고 판단하고 최적화를 취소(De-optimization)한다.

## 🤓 Answer

109.987ms // When updating the 0th element, the array switched from the SMI type to the DOUBLE type, and this transition took the same amount of time as filling the 10_000_000 array with numbers!

With update of the 0th and 1th elements:

arr[0] = 0.1;
arr[1] = 10;

105.085ms // Uncommenting the update of the first element did not make any difference in the speed of the application, since no type transition occurred.

With update of the 0th, 1th, 2th elements:

arr[0] = 0.1;
arr[1] = 10;
arr[2] = '10';

193.61ms // **Another action we took increased the execution time by 2 times, since the transition was made again. This time from the DOUBLE_ELEMENTS type to the more general ELEMENTS type.**

With update of the 0th, 1th, 2th, 3th elements:

arr[0] = 0.1;
arr[1] = 10;
arr[2] = '10';
arr[3] = { a: 'hello' };

196.361ms // As expected, the time did not change much, since there was no type transition.

## 📄 Reference

> "더 일반적인 ELEMENTS 타입"은 V8 엔진이 다양한 타입의 요소를 처리할 수 있도록 배열을 최적화하는 방법 중 하나입니다. 배열에는 처음에는 특정한 타입의 요소만 들어가 있을 수 있습니다. 예를 들어, 모든 요소가 정수일 경우 'SMI'라고 불리는 특수한 최적화 타입을 사용할 수 있습니다. 또는 모든 요소가 부동 소수점일 경우 'DOUBLE_ELEMENTS' 타입을 사용할 수 있습니다. <br />
> 그러나 배열에 다양한 타입의 요소가 들어가게 되면, V8 엔진은 이를 일반적으로 처리할 수 있도록 내부 구조를 변경합니다. 이것을 "ELEMENTS" 타입으로 전환하는 것입니다. 이 타입은 배열 내부의 요소가 어떤 타입이든 처리할 수 있도록 해줍니다. 이로 인해 타입 전환이 더 이상 필요하지 않게 되므로, 후속 작업에서는 실행 시간이 크게 증가하지 않습니다.
