# Q26. Which loop will run faster?

## ❓ Question

```js
const strPrimitive = generateRadonString(100_000);
const strObject = new String(generateRandomString(100_000));

console.time("primitive");
for (let i = 0; i < 100_000; i++) {
  strPrimitive.slice(i);
}
console.timeEnd("primitive");

console.time("object");
for (let i = 0; i < 100_000; i++) {
  strObject.slice(i);
}
console.timeEnd("object");
```

- [x] primitive
- [] object
- [] same time

## 🤔 My Thinking

원시 문자열과 문자열 객체는 자바스크립트 상에서 다르게 처리된다. 원시 문자열은 문자열을 처리하는 데에 필요한 최소한의 정보만을 메모리 캐싱하고 있다. 이로 인해 메모리 사용량이 적고, 작업을 빠르게 수행할 수 있다. <br />
반면에 문자열 객체는 메타데이터(프로토타입, 생성자 등의 내장 속성)와 메서드 등 추가적인 정보를 가지고 있어 원시 문자열보다 더 많은 메모리를 차지한다. 또한, 메서드를 호출할 때마다 이러한 추가 정보를 하므로 작업 속도가 느려질 수 있다.

<br />

메모리 사용량이 성능에 직접적인 영향을 미치는 사항은 다음과 같다:

- 캐시 효율성: 메모리가 적게 사용되면, 데이터는 CPU 캐시에 더 효율적으로 저장될 수 있습니다. 캐시에 더 많은 데이터가 들어갈 수록, CPU가 RAM으로의 접근을 덜 하게 되므로 성능이 향상됩니다.

- 데이터 전송 시간: 메모리 사용량이 적을수록, 데이터를 메모리에서 CPU로 (또는 그 반대로) 전송하는 데 필요한 시간이 줄어듭니다. 이는 작업의 전체 실행 시간을 줄일 수 있습니다.

- 페이지 폴트: 메모리 사용량이 적으면 페이지 폴트(Page Fault)가 덜 발생합니다. 페이지 폴트는 디스크에서 데이터를 메모리로 불러와야 할 때 발생하는데, 이 과정은 상대적으로 느립니다.

- 병렬 처리: 메모리 사용량이 적으면 여러 작업을 동시에 처리하기 더 쉽습니다. 이는 멀티코어 프로세서에서 특히 유용합니다.

- 가비지 컬렉션: 객체가 적은 메모리를 사용하면, 가비지 컬렉터가 덜 자주 동작합니다. 가비지 컬렉션이 빈번하게 발생하면, 그 오버헤드로 인해 애플리케이션의 성능이 저하될 수 있습니다.

- 알고리즘 복잡도: 메모리 사용이 적은 데이터 구조는 종종 더 단순한 알고리즘을 사용할 수 있게 합니다. 복잡한 알고리즘은 더 많은 연산을 필요로 하므로, 이 경우에도 메모리 사용량이 적은 것이 이점이 될 수 있습니다.

## 🤓 Answer

Explanation.

How is a property accessed in the case of a primitive string?

You may have heard that when you try to read a property or method from a primitive string, such as str.slice(i), **the browser creates a wrapper String object, accesses the requested property, and when the wrapper object is no longer needed, it removes it.**

Based on this, we can assume that over a large number of iterations, due to the constant creation and removal of wrapper objects, the efficiency of the primitive string will be lower than the object string.

**In fact, the browser JS engine does not always create a wrapper object when accessing a property or method of a primitive string. Instead, it has so-called short paths, when, seeing a call to a certain property or method, it immediately returns what it is looking for without creating a wrapper object.**

In almost 100% of cases, a primitive string is preferable to use over an object string.

primitive: 1.926ms
object: 11.095ms

## 📄 Reference

> https://hacks.mozilla.org/2012/12/performance-with-javascript-string-objects/
