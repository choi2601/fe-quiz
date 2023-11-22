# Q41. Which line will cause an error in typescript?

## ❓ Question

```ts
function setValue(val: number) {
  let res = val > 0 ? val : "wrong number";

  if (typeof res === "string") {
    console.log(`Error: ${res}`);
    res = false;
  } else {
    res = "OK";
  }

  return res;
}
```

- [] let res = val > 0 ? val : "wrong number";
- [x] res = false;
- [] res = "OK";
- [] res = false; and res = "OK";

## 🤔 My Thinking

타입스크립트에서 변수의 타입은 처음 할당 시에 결정된다. 조건부(삼항) 연산자에 의해 val의 타입 string | number 유니온 타입으로 추론된다.

false는 boolean 타입이기 때문에 string | number 유니온 타입인 변수에 할당할 수 없다.

## 🤓 Answer

Explanation.

When we declare a variable with an assignment, typescript looks at the right side and types the variable with the appropriate type.

This also applies to cases where the right-hand expression can take on different types depending on the runtime value of the variable. In this case, the result type of the expression will be a union.

let res = val > 0 ? val : 'wrong number'; // let res: string | number

Whenever you change the variable further, typescript checks that the new value matches the union type.

res = 'OK'; // works because type string is included in the union string | number

res = false; // throws an error because boolean is not included in the union string | number

Type 'boolean' is not assignable to type 'string | number'.
