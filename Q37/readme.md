# Q37. What type is used incorrectly?

## ❓ Question

```ts
interface IUser {
  id: number;
  name: string;
}

interface IUser {
  role?: "user" | "admin";
}

const user: IUser = { id: 1, name: "Kevin", role: "admin" };

type Shape = {
  width?: number;
  height?: number;
};

type Shape = {
  radius?: number;
};

const circle: Shape = { radius: 10 };
```

- [] IUser
- [x] Shape
- [] both
- [] none

## 🤔 My Thinking

인터페이스 타입은 보강(argument)가 가능하다.

위 예시 코드와 같이 속성을 확장하는 것을 선언 병합(declaration merging)이라고 한다.

선언 병합은 주로 타입 선언 파일에서 사용된다. 따라서 타입 선언 파일을 작성할 때는 선언 병합을 지원하기 위해 반드시 인터페이스를 사용해야 하며 표준을 따라야 한다.

타입 선언에는 사용자가 채워야 하는 빈틈이 있을 수 있는 데, 선언 병합이 이에 해당된다.

타입스크립트는 여러 버전의 자바스크립틍 표준 라이브러리에서 여러 타입을 모아 병합된다. 예를 들어 Array 인터페이스는 `lib.es5.d.ts`에 정의되어 있고 기본적으로는 lib.es5.d.ts에 선언된 인터페이스가 사용된다.

그러나 tsconfig.json의 lib 목록에 `ES2015`를 추가하면 타입스크립트는 lib.es2015.d.ts에 선언된 인터페이스를 병합한다. 여기에는 ES2015에 추가된 또 다른 Array 선언의 find 같은 메서드가 포함된다.

이들은 병합을 통해 다른 Array 인터페이스에 추가된다. 결과적으로 각 선언이 병합되어 전체 메서드를 가지는 하나의 Array 타입을 얻게 된다.

## 🤓 Answer

Explanation.

Properties can be added to the interface after creation.

A type cannot be changed after creation; an error will be thrown when declaring the type twice.

Duplicate identifier 'Shape'.
