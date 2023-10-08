# Q19. Which 2 users will faster than others?

## ❓ Question

```js
function render({ name, active }) {
  return `User ${name}: Active: ${active}`;
}

const users = [
  { name: "John", active: false },
  { name: "Mike", active: true },
  Object.assign(
    {},
    {
      name: "Harry",
      active: true,
    }
  ),
  Object.assign(
    {},
    {
      name: "Alex",
      active: false,
    }
  ),
];

users.map((user, i) => {
  console.time(i);
  render(user);
  console.timeEnd(i);
});
```

- [ ] John, Mike
- [ ] Harry, Alex
- [ ] John, Harry
- [ ] Mike, Alex

## 🤔 My Thinking

`Object.assign` 기본 객체 리터럴에 기존 객체를 추가하여 새로운 객체를 만들어 내지만, 해당 연산이 단순히 템플릿 문자열을 반환하는 render 함수 성능에 큰 영향을 주진 못할 것이다.

## 🤓 Answer

Explanation.

The execution time on my device when running in a v8 environment looks like this:

0: 0.075ms
1: 0.005ms
2: 0.042ms
3: 0.005ms

Let's try to figure it out.

The first time a function is called, it is executed without any optimizations from the engine. Therefore, the execution time for the first call is obviously the longest.

Next, the engine optimizes the function and all further calls will be faster. But there is still a slight difference in execution speed from call to call. On the second and fourth calls, the function executes faster and the reason for this is inline caching.

To understand how inline caching works, you first need to understand how objects are stored in memory.

Let's look at an example:

```js
var a = { x: 10, y: 20 };
var b = { x: 15, y: 25 };
```

To implement reading and rewriting property values ​​in objects, we need to know where they are stored. How to implement this?

We could store the addresses of these 4 properties a.x, a.y, b.x, b.y separately somewhere in the hashmap. However, this approach requires a lot of space.

Instead, for all objects with the same structure, we can store the property addresses once - as an offset relative to the beginning of the object.

So we can say that for all objects of the form { x: int, y: int }, the x property is stored at offset 0 and the y property is stored at offset 4 relative to the beginning of the object. And then store only the addresses of the beginning of objects. This form of storage is much more compact, especially when there are many identical objects.

This approach is called hidden classes and is implemented under different terminology by all modern browsers (in v8 terminology this is called maps).

Hidden classes make inline caching possible.

Inline caching allows us to quickly access object properties.

When the function is called for the first time, the engine remembers at what offset the properties used by the function are located in the object. When further calls to the function are made using the same hidden class (if it has not changed), the engine does not go looking for where this or that property is located, but takes it from the saved offset. This saves time, especially if the function is called with the same hidden class many times.

When calling render() for the first time

```js
render({ name: "John", active: false });
```

the engine filled the hidden class of the object and saved the address of the name and active properties.

On the second call

render({ name: 'Mike', active: true });

it used this information to quickly access the object's fields since it has the same hidden class.

The third time

```js
render(
  Object.assign(
    {},
    {
      name: "Harry",
      active: true,
    }
  )
);
```

The engine was unable to apply inline caching.

At first glance, these objects look similar, but have different hidden classes.

The object `{ name: 'Mike', active: true }` is created with 2 properties name and active and has a corresponding hidden class.

An object created using `Object.assign({}, {
name: 'Harry',
active: true
})` was initially empty, and then the name and active properties were added to it one by one - this is how Object.assign works.

Therefore, the hidden class of this object could not reuse the existing one, it changed gradually - at first it was empty, then it evolved into a class with the name property, then into a class with two properties - name and active.

On the fourth call

```js
render(
  Object.assign(
    {},
    {
      name: "Alex",
      active: false,
    }
  )
);
```

object creation goes through the same steps as the third call. However, now at each stage, the intermediate object shares a hidden class with the one that was created for the object from the third class at the corresponding stage. Thus, inline caching was also applied here and therefore this call is slightly faster than the previous one.

You can check whether objects have the same hidden class by running node.js with the --allow-natives-syntax flag and using the native %HaveSameMap function:

```js
console.log(
  %HaveSameMap({ name: "John", active: false }, { name: "Mike", active: true })
); // true
```

## 📄 Reference

> https://engineering.linecorp.com/ko/blog/v8-hidden-class
