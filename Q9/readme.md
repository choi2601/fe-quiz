# Q9. Which loop is more efficient?

## ❓ Question

```js
let list = document.querySelector(".list");

// A loop
for (let i = 0; i < 100_000; i++) {
  let li = document.createElement("li");
  li.textContent = i;
  list.appendChild(li);
}

// B loop
let documentFragment = document.createDocumentFragement();

for (let i = 0; i < 100_000; i++) {
  let li = document.createElement("li");
  li.textContent = i;
  documentFragment.appendChild(li);
}

list.appendChild(documentFragment);
```

- [ ] A loop
- [x] B loop
- [ ] roughly equivalent

## 🤔 My Thinking

DocumentFragment는 DOM의 단편적인 부분을 정의할 수 있는 노드이다. 기본적으로 DOM과 동일하게 동작하지만, HTML의 DOM 트리에는 영향을 주지 않으며 메모리에서만 정의된다. 메모리 상에서만 존재한다는 점에서, 리액트에서의 가상 돔과 비슷한 개념으로 볼 수 있다. <br />
A 루트는 list 요소에 직접 자식 요소를 추가할 때마다 브라우저의 렌더링 큐에 변화 사항이 적재되기 때문에 지속적으로 레이아웃을 다시 계산하거나 웹 페이지를 재렌더링해야 될 수 있다. <br />
반면 documentFragment는 실제 DOM을 조작하는 것이 아닌 메모리 상에서 존재하기 때문에 모든 리스트 아이템이 프로그래먼트에 추가된 후, 해당 프레그먼트가 list 요소에 한 번에 추가되기 때문에 더 효율적이다.

## 🤓 Answer

Explanation.

**Modern browsers optimize adding elements to the DOM by aggregating the changes and doing only one reflow and one paint each. Therefore, using DocumentFragment will not give you a performance advantage.**

Here is what MDN writes about this:

_The performance benefit of DocumentFragment is often overstated. In fact, in some engines, using a DocumentFragment is slower than appending to the document in a loop as demonstrated in this benchmark._

However, DocumentFragment can still be useful when we need to assemble a piece of code and add it in many places.

Without DocumentFragment:

```js
const elements = [];
const lists = document.querySelectorAll(".list");

for (let i = 0; i < 10_000; i++) {
  const li = document.createElement("li");
  li.innerText = i;
  elements.push(li);
}

for (let i = 0; i < lists.length; i++) {
  for (let j = 0; j < elements.length; j++) {
    lists[i].appendChild(elements[j].cloneNode(true));
  }
}
```

With DocumentFragment:

```js
let documentFragment = document.createDocumentFragment();

for (let i = 0; i < 10_000; i++) {
  const li = document.createElement("li");
  li.innerText = i;
  documentFragment.appendChild(li);
}

for (let i = 0; i < lists.length; i++) {
  lists[i].appendChild(documentFragment.cloneNode(true));
}
```

Using DocumentFragment in this case helped us avoid a nested loop.
This script will run faster

## 📄 Reference

> https://developer.mozilla.org/ko/docs/Web/API/Document/createDocumentFragment
