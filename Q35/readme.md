# Q35. How to type myObj so that typescript doesn't throw an error?

## ❓ Question

```ts
let myObj = { x: "hello" };

myObj.y = 12;

console.log(myObj);
```

- [] leave as is
- [] unknown
- [] { x: string; }
- [] { x: string; y: number; }
- [x] all options are invalid

## 🤔 My Thinking

myObj는 처음 객체 리터럴 `{ x: "hello" }`을 할당할 때, `{ x: string }` 으로 타입 추론을 한다.

위 맥락 과정에서 보았을 때, `myObj.y = 12` 와 같은 number 타입의 새로운 속성 y를 추가하기 위해서는 다음과 같은 방법이 있다.

- 선택적 속성: y 속성을 선택적(optional)로 만든다.

```ts
let myObj: { x: string; y?: number } = { x: "hello" };
myObj.y = 12;
```

- 인덱스 시그니처: 객체가 다양한 속성을 가질 수 있도록 인덱스 시그니처를 사용할 수 있다.

```ts
let myObj: { [key: string]: string | number } = { x: "hello" };
myObj.y = 12;
```

## 🤓 Answer

Explanation.

Let's practice typescript a little.

There are the following options to add properties to an object dynamically in typescript:

1. The object must be of type any.

```ts
let myObj: any = { x: "hello" };
myObj.y = 12;
console.log(myObj);
```

Using any disables all further type checking, so this is the least desirable option.

2. Type, which says that an object can have any properties.

```ts
let myObj: { [key: string]: any } = { x: "hello" };
myObj.y = 12;
console.log(myObj);
```

If you know that property values ​​can be either strings or numbers.

```ts
let myObj: { [key: string]: string | number } = { x: "hello" };
myObj.y = 12;
console.log(myObj);
```

3. Type with optional fields.

```ts
let myObj: { x: string; y?: number } = { x: "hello" };
myObj.y = 12;
console.log(myObj);
```

The best choice. Essentially, with this approach, the property is no longer dynamic.

The dynamic nature of JavaScript can be convenient for developers, but at the same time it is difficult for compilers (it is more difficult to optimize) and often leads to bugs. By using typescript correctly, we can avoid all these disadvantages.
