# Q34. What UserId type is correct for the id argument of the `userInfo()` function?

## ❓ Question

```ts
function userInfo(id: UserId) {
  if (id === 0) {
    return "Bot";
  }

  return `User id: ${id.toUpperCase()}`;
}
```

- [] type UserId = string;
- [] type UserId = number | string;
- [x] type UserId = 0 | string;
- [] none

## 🤔 My Thinking

userInfo 함수를 보면, id 인자에 대해 두 가지 타입의 연산을 수행하고 있다.

첫 번째 `if(id === 0) { ... }` 연산식에선 id가 숫자 타입이 들어올 수 있음을 암시하고 있으며 두 번째 연산 `String.prototype.toUpperCase()` 메서드를 통해 id는 반드시 문자열이어야 함을 드러낸다.

하지만 `string | number` 유니온 타입은 id의 값이 0이 아닌 경우에도 여전히 id 타입 값이 number 임을 추론하기 때문에 마찬가지로 타입 에러가 발생할 것이다.

이 경우엔 집합의 관점에서 number 타입보단 0으로 타입을 좁게 설정하는 것이 좋을 것이다.

## 🤓 Answer

Explanation.

Using the toUpperCase() method in the return statement hints to us that the id parameter that is being used this line must be of type string.

However, if we use string for the argument, typescript will throw an error when we try to compare the string with 0 in the line

if (id === 0) // This condition will always return 'false' since the types 'string' and 'number' have no overlap.

When the value of a variable can be of different types, we use a union type.

A union type describes a value that can be one of several types.

type UserId = number | string;

This data type is also incorrect for use in this example. Because there is no check in the function that the last line should only be executed with an id of type string, typescript will throw an error:

return `User id: ${id.toUpperCase()}`; // Property 'toUpperCase' does not exist on type 'number'.

type UserId = 0 | string;

With this type of id variable, the id value in the last return statement will always be of type string and typescript will have nothing to complain about.
