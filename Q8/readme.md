# Q8. When will the browser download the image?

## ❓ Question

```html
<html>
  <head>
    <link rel="preload" href="./bg.jpeg" />
  </head>
  <body>
    <script>
      setTimeout(() => {
        const img = document.createElement("img");
        img.src = "./bg.jpeg";
        document.body.appendChild(img);
      }, 1000);
    </script>
  </body>
</html>
```

- [x] when the link tag is processed
- [ ] when the script is processed
- [ ] when the setTimeout callback is executed
- [ ] never

## 🤔 My Thinking

`rel=preload` 속성을 통해 페이지에 필요한 리소스를 지정하고 브라우저의 렌더링 시퀀스가 실행되기 전에 리소스를 참조할 수 있다. <br />
delay 시간이 흐르고 setTimeout 내 콜백이 실행되었을 때 사전에 참조되어진 이미지가 즉각적으로 DOM에 추가가 된다.

## 🤓 Answer

Explanation.

**The browser will add the image to the download queue only when it encounters it**, executing the setTimeout callback.

**This is exactly what a link with rel="preload" is meant to avoid.**
However, in this case it did not work due to incorrect use and the browser behaved as if it did not exist.

The link tag, which acts as a preloader, has a mandatory as attribute, which we missed.

For the preload to work correctly, you need to add an as attribute with the value image:

```html
<link rel="preload" href="./bg.jpeg" as="image" />
```

Now the browser will add the image to the queue for downloading earlier - when it processes the link tag.

## 📄 Reference

> https://developer.mozilla.org/ko/docs/Web/HTML/Element/link
