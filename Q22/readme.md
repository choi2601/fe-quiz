# Q22. Which array takes the most time to create and fill?

## ❓ Question

```js
console.time("first");
const arr = new Array(1000);
for (let i = 0; i < arr.length; i++) {
  arr[i] = i;
}
console.timeEnd("first");

console.time("second");
const arr2 = [];
for (let i = 0; i < 1000; i++) {
  arr2[i] = i;
}
console.timeEnd("second");

console.time("third");
const arr3 = [];
for (let i = 0; i < 1000; i++) {
  arr3.push(i);
}
console.timeEnd("third");
```

- [] first
- [] second
- [x] third
- [] same times

## 🤔 My Thinking

first 같은 경우 `Array.from`을 통해 미리 배열의 크기를 정하고 메모리를 할당하기 때문에 더 빠를 수 있다. <br />
다만, second와 third 방식 모두 요소가 추가될 때마다 동적으로 메모리를 재할당해야 하는 방식이기 때문에 연산 과정이 first에 비해 느릴 수 있다. <br />
특히 third는 메서드 호출 오버헤드(method call overhead)로 가장 느릴 수 있다. <br />

메서드 호출 오버헤드는 메서드(또는 함수)를 호출할 때 발생하는 추가적인 시간 또는 리소스를 의미하는데, 다음과 같은 사항이 추가적으로 요구될 수 있다.

- 스택 프레임 생성: 함수 호출이 발생할 때마다 새로운 스택 프레임이 생성되어 로컬 변수, 반환 주소 등을 저장

- 인수 전달: 메서드에 전달되는 인수가 있을 경우, 이들을 스택에 넣거나 레지스터에 저장하는 작업이 필요

- 컨텍스트 스위칭: 메서드 내부에서 다른 메서드를 호출하거나, 재귀 호출을 하는 등의 작업이 발생할 때 컨텍스트(상태)를 저장하고 복원해야 할 필요가 있음

- 반환 값 처리: 메서드가 값을 반환할 경우, 이 값을 호출자에게 전달하기 위한 작업이 필요

## 🤓 Answer

Explanation.

We will talk about the V8 engine, but tests in browsers other than Chrome have similar (Firefox) or at least not contradictory (Safari) results.

Since when creating an array using the Array constructor, the array is created with a given length, but without elements, **it is assigned the type SMI_HOLEY_ELEMENTS. HOLEY - due to the lack of elements, SMI - as the most likely type of future elements.**

Next we actually fill the array with integers.

**The array becomes packed, however, it does not change its type from SMI_HOLEY_ELEMENTS to SMI_PACKED_ELEMENTS, since type transformation is possible only as a refinement, from a more general to a more specific one. Therefore, this array will never become PACKED again.**

**All built-in functions are optimized for different data types. For more precise data types - better optimizations. Code for packed arrays will run faster than code for arrays with holes.**

In the example, the two remaining code options for filling the array initially work with an empty array, and therefore do not have this problem.

Loop times in node:

first: 0.199ms
second: 0.049ms
third: 0.047ms

## 📄 Reference

> https://v8.dev/blog/elements-kinds?m=1

> V8 엔진은 성능 최적화를 위해 배열의 '타입'을 추적합니다. 배열이 생성될 때 타입이 할당되고, 이후에도 이 타입은 "더 일반적인 타입에서 더 구체적인 타입으로"만 세밀화(refinement) 될 수 있습니다.<br /> 즉, 일단 배열이 'HOLEY' 타입으로 설정되면, 그 이후에 'PACKED' 상태로 변경되더라도 이전에 'HOLEY'였다는 사실 때문에 타입이 'HOLEY'로 유지됩니다. <br /> 이러한 설계의 이유 중 하나는, 배열의 타입을 빈번하게 변경하면 그에 따른 오버헤드가 커질 수 있기 때문입니다. 예를 들어, 배열의 타입을 변경할 때마다 다양한 내부 데이터 구조와 메타데이터를 업데이트해야 할 수 있으며, 이는 성능에 부정적인 영향을 미칠 수 있습니다. <br /> 또한, V8은 타입에 따라 배열 연산에 대한 다양한 최적화 경로를 가집니다. 배열이 한 번 'HOLEY' 타입으로 설정되면, 이후에 그 배열에 대한 연산은 'HOLEY' 타입에 최적화된 코드 경로를 사용할 것입니다. <br /> 만약 타입이 빈번하게 변경된다면, 이러한 최적화 경로를 선택하는 것이 복잡해질 수 있습니다. 이러한 이유로, V8 엔진은 배열의 타입을 가능한 한 일관되게 유지하려고 합니다.
