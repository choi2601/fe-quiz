# Q38. Assigning a value to which variable will throw an error in typescript?

## ❓ Question

```ts
let a;
a = 1;
a = "hello";

let b = 1;
b = "hello";
```

- [] a
- [x] b
- [] both
- [] none

## 🤔 My Thinking

변수 a는 타입을 명시적으로 선언하지 않고 `let a;`로 선언하였다.
타입스크립트는 이 경우 a를 `any` 타입으로 추론한다. any 타입은 어떤 타입의 값도 할당할 수 있기 때문에, 오류가 발생하지 않는다.

반면에, 변수 b는 선언과 동시에 1로 초기화된다. 타입스크립트는 b의 타입을 `number`로 추론하기 때문에 이후 `string` 타입의 할당에서 타입 에러가 발생할 것이다.

## 🤓 Answer

Explanation.

When we declare a variable with an assignment, typescript looks at the right side and types the variable with the appropriate type.

let b = 1; // let b: number

When you further try to assign a value of a different type to the variable, typescript throws an error.

b = 'hello'; // Type 'string' is not assignable to type 'number'.

When you declare a variable without assigning a value, the variable is of type any. Which means it can take on different types of values.

let a; // let a: any;

Note that the noImplicitAny rule does not prohibit this behavior. It only applies to cases where typescript cannot guess the type of a variable. For example, this applies to function parameters.

// Parameter 'x' implicitly has an 'any'
// Parameter 'y' implicitly has an 'any'
function pow(x, y) {
return x \* y;
}

On the other hand, in the example, typescript correctly determines the type of variable a at each stage of its existence and does not allow actions that are not possible with this type.

let a;
a = 1;
// Property 'toUpperCase' does not exist on type 'number'.ts(2339)
console.log(a.toUpperCase());
a = 'hello';
console.log(a.toUpperCase()); // correct
