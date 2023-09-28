# Q15. What is the best browser hint to speed up the aggregation of airline tickets from different origins?

## ❓ Question

- [ ] preload
- [ ] prerender
- [x] preconnect
- [ ] prefetch

## 🤔 My Thinking

`preconnect`는 웹 브라우저에게 특정 도메인에 대한 연결을 미리 준비하도록 지시하는 브라우저 힌트이다. <br />
이는 DNS 조회, TCP 핸드셰이크, TLS 네고시에이션과 같은 연결 설정 단계를 미리 완료하게 해준다. 그 결과, 실제 자원을 요청을 할 때 시간을 절약할 수 있다. <br />

하나의 웹 페이지가 여러 출처(origin)에서 여러 항공사의 티켓 정보를 집계하는 경우, 각각 다른 웹 서버나 도메인에 대해서 연결을 미리 설정할 수 있게 하는 `preconnect`
속성을 사용한다면 빠른 리소스 응답을 받을 수 있을 것이다.

## 🤓 Answer

Explanation.

Your goal is to speed up the display of user search results for airline tickets. You cannot prerender this page because it is entirely composed of dynamic content that you will receive from external resources. You also cannot prefetch this data before the user enters search parameters.

In this case, the preconnect hint is best.

**The preconnect keyword for the rel attribute of the `<link>` element is a hint to browsers that the user is likely to need resources from the target resource's origin, and therefore the browser can likely improve the user experience by preemptively initiating a connection to that origin. Preconnecting speeds up future loads from a given origin by preemptively performing part or all of the handshake (DNS+TCP for HTTP, and DNS+TCP+TLS for HTTPS origins).**

```html
<link rel="preconnect" href="https://example.com" />
```

Since your airline ticketing application needs to connect to many different origins, doing this upfront will save you a significant amount of time when the user makes a request.

## 📄 Reference

> https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/rel/preconnect

> https://web.dev/preconnect-and-dns-prefetch/
