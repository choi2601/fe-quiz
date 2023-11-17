# Q36. Which user's logging will throw an error?

## ❓ Question

```ts
interface IUser {
  id: number;
  name: string;
  role: "user" | "admin";
}

const logUser = (user: IUser) => console.log(`${user.name}, ${user.id}`);

const john = {
  id: 1,
  name: "John",
  role: "admin",
};

logUser(john);

logUser({
  id: 2,
  name: "Alex",
  role: "user",
});
```

- [x] John
- [] Alex
- [] both
- [] none

## 🤔 My Thinking

> TypeScript의 타입 호환성은 구조적 서브타이핑(structural subtyping)을 기반으로 합니다.
> 구조적 타이핑이란 오직 멤버만으로 타입을 관계시키는 방식입니다.
> 명목적 타이핑(normal typing)과는 대조적입니다. TypeScript의 구조적 타입 시스템의 기본 규칙은 y가 최소한 x와 동일한 멤버를 가지고 있다면 x와 y는 호환된다는 것입니다.

타입스크립트는 타입 호환성을 지원한다.

```ts
type Coffee = {
  cafeIn: number;
  fat: number;
};

// 명목목 서브타이핑(nominal subtyping)
type Latte = Coffee & {
    milk: number;
}

function calculateCafeIn(coffee: Coffee) {
    ( ... )
}

const latte1: Latte = {
    cafeIn: 10;
    fat: 30;
    milk: 4;
}

// 구조적 서브타이핑(structural subtyping)
const latte2 = {
    cafeIn: 20;
    fat: 10;
    milk: 3;
}

// 정상 동작
calculateCafeIn(latte1);
calculateCafeIn(latte2);

```

위의 예시 코드와 같와 타입스크립트 타입 시스템은 부분적으로 타입 호환을 지원다.

즉, 타입스크립트의 타입 시스템은 덕 타이핑(Duck Typing)에 기반한다.

덕 타이핑(duck typing)이란 객체의 형태(shape)가 어떤 인터페이스에 정의된 형태와 일치하면, 그 객체를 해당 인터페이스 타입으로 간주한다는 것이다.

구조적 서브타이핑은 상속 관계가 명시되어 있지 않더라도 객체의 프로퍼티를 기반으로 사용처에서 사용함에 문제가 없다면 타입 호환을 허용하는 방식입니다.

하지만 아래의 예시 코드는 타입 호환이 지원되지 않는다.

```ts
calculateCafeIn({
  cafeIn: 40,
  fat: 50,
  milk: 60,
});
```

타입스크립트는 초기 객체 리터럴(object literal)를 `Fresh Literal`로 간주한다.
이후 타입을 단언(type assertion)을 하거나, 타입 추론에 의해 객체 리터럴의 타입이 확장되면 *freshness*가 사라지게 된다.

특정한 변수에 객체 리터럴을 할당하는 경우 위 두 가지 중 한 가지가 발생하게 되므로, *freshness*가 사라지게 되며, 함수에 인자로 객체 리터럴을 바로 전달하는 경우에는
*fresh*한 상태로 전달된다.

즉, 객체 리터럴을 변수에 할당하거나 함수에 매개변수로 전달할 경우 타입 호환을 허용하지 않고 **잉여 속성 체크(Excess Property Checking)**가 수행된다.

## 🤓 Answer

Explanation.

Calling logUser() with the argument john will throw an error due to a role property type mismatch.

Argument of type '{ id: number; name: string; role: string; }' is not assignable to parameter of type 'IUser'.
Types of property 'role' are incompatible.
Type 'string' is not assignable to type '"user" | "admin"'.

Despite the fact that the role property of the john object has the value 'admin', which satisfies the type 'user' | 'admin', typescript identifies it as a string.

The thing is that the properties of an object can change and typescript cannot be sure that at the time the function is called, the value of the property still satisfies the type.

There is no such problem when calling the logUser() function the second time, because the object is created at the place where the function is called, the property has no opportunity to change.

To ensure that the first call works correctly, you can specify the type of the role property when creating the john object.

const john = {
id: 1,
name: 'John',
role: 'admin' as 'user' | 'admin'
};

Then an attempt to change a property to an invalid value will result in an error, and at the time of calling the logUser() function, typescript will be sure that the property has the desired type.

john.role = 'abc'; // Type '"abc"' is not assignable to type '"user" | "admin"'.

## 📄 Reference

> https://toss.tech/article/typescript-type-compatibility
