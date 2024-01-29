# Q65. What will be the output?

## ❓ Question

```js
// module.js
export const foo = Promise.resolve("foo");
export const bar = Promise.resolve("bar");

// index.js
let foo, bar;

(async () => {
  ({ foo } = await import("./module.js"));
})();

console.log(foo);

({ bar } = await import("./module.js"));

console.log(bar);
```

- [] `foo bar`
- [] `Promise{'foo'} Promise{'bar'}`
- [] `undefined undefined`
- [] `undefined bar`
- [] `undefined Promise{'bar'}`

## 🤓 Answer

Explanation.

The import() call, commonly called dynamic import, is a function-like expression that allows loading an ECMAScript module asynchronously and dynamically.

import(module) returns a promise which fulfills to an object containing all exports from module.

Because exported values ​​are promises, the variables foo and bar will contain promises. To get the value of promises, you need to wait for them to be completed using another await keyword or then() handler.

```js
console.log(bar); // Promise {'bar'}
console.log(await bar); // bar
```

It is also possible to wait for promises to be fulfilled in the exporter module.

```js
module.js;
export const bar = await Promise.resolve("bar");

index.js(({ bar } = await import("./module1.mjs")));

console.log(bar); // bar
```

The import of the foo variable is additionally wrapped in an asynchronous function. Since we are not waiting for the function to execute (there is no await keyword before calling the function), undefined will be printed to the console.

```js
(async () => {
  ({ foo } = await import("./module1.mjs"));
})();

console.log(foo); // undefined
```

Fix:

```js
await (async () => {
  ({ foo } = await import("./module1.mjs"));
})();

console.log(foo); // Promise {'foo'}
```
