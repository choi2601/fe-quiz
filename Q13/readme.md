# Q12. When will the browser download the font?

## ❓ Question

```html
<html>
  <head>
    <link rel="preload" href="./regular.woff2" as="font" />
    <style>
      @font-face {
        font-family: "PT Sans";
        font-style: normal;
        font-weight: 400;
        src: url("./regular.woff2") format("woff2");
      }
      .text {
        font-family: "PT Sans";
        font-size: 14px;
      }
    </style>
  </head>
  <body>
    <div class="test"></div>
  </body>
</html>
```

- [x] when the link tag is processed
- [ ] when @font-face is processed
- [ ] when .text class is processed
- [ ] when .text class is applied to the div element
- [ ] never

## 🤔 My Thinking

[Q8 문제](../Q8/readme.md)와 같이 `as=font` 속성과 같이 `rel=preload`를 사용하게 된다면 브라우저는 해당 리소스가 폰트 파일임을 인식하고 HTML 문서를 처음 로드할 때 link 태그가 처리되면서 폰트가 다운로드될 것이다.

## 🤓 Answer

Explanation.

In this example, we are prompting the browser to download the font before the browser parses the html and finds its use on its own.

In the same way, we can tell the browser to download any resource in advance: styles, script, image, etc. This feature is especially relevant when the resource cannot be detected by the browser immediately in the root html, but is located somewhere deep in the script or styles.

Using rel="preload" ensures that resources become available sooner and are less likely to block page rendering, which improves performance.
