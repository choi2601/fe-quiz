# Q5. Which css property speeds up the initial rendering of the page?

## ❓ Question

- [x] content-visibility
- [ ] isolation
- [ ] will-change

## 🤔 My Thinking

content-visibility를 사용하게 될 경우 DOM 내 서브 트리의 렌더링을 제어할 수 있다. <br />
예를 들어, 어떤 엘리먼트에 `content-visibility: auto`를 설정할 경우 해당 엘리먼트는 화면(viewport)에 보일 때만 <br /> 브라우저가 렌더링하게 되므로
초기 페이지 로딩(FCP)이 더 빨라진다.

## 🤓 Answer

Explanation.

Just one property can speed up page rendering many times.
This property is content-visibility.

How to use:

1. Break your page into blocks.
2. Apply to each block content-visibility: auto.

The browser will style and layout all of the contents that are currently visible to the user. When processing the block that is fully off-screen, the browser will skip the rendering work and only style and layout the element box itself.

On our landing page, we were able to achieve a 3x speedup of initial rendering with the help of the content-visibility property.

## 📄 Reference

> https://web.dev/content-visibility/

> https://web.dev/i18n/ko/fcp/
