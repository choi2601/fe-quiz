# Q6. Which animation is more efficient?

## ❓ Question

```css
.transform {
  transform: translate(0px, 100px);
  transition: transform 3s;
}

.position {
  top: 100px;
  transition: top 3s;
}
```

<br />

- [x] transform
- [ ] position
- [ ] roughly equivalent

## 🤔 My Thinking

CLS는 페이지의 전체 수명동안 발생하는 모든 예기치 않은 레이아웃 이동에 대해 가장 큰 레이아웃 이동 점수 버스트를 뜻한다. <br />
레이아웃 이동은 시각적 요소가 렌더링된 프레임에서 다음 프레임으로 위치를 변경할 때마다 발생한다. <br />
이러한 layout-shift는 operation 단계 중 layout 단계를 재구성한다. 이 말은 즉슨 paint 단계에서 각각의 요소에 대해서 잘게 나눈 이미지(BitMap)을 다시 준비하기 때문에 전체적인 효율성이 저하된다는 것이다.

<br>

레이아웃 이동은 기존 요소가 시작 위치를 변경할 때만 발생한다. 새 요소가 DOM에 추가되거나 기존 요소의 크기가 변경되면 변경으로 인해 가시적 요소의 시작 위치가 변경되지 않는 한 레이아웃 이동으로 간주하지 않는다. <br />
transform은 요소의 시작 위치 자체를 변경하지 않고 composition 단계에서만 변화가 일어나기 때문에 효율적이다.

## 🤓 Answer

Explanation.

When rendering a page, the browser splits it into layers, rasterizes each layer
(translates html and css data into pixels) separately, and then composites the resulting layers. This is necessary to optimize operations such as scrolling.

When scrolling, a new piece of the page appears in the viewport, and it will be enough for the browser to recompose the already drawn layers in order to show what is necessary in the viewport, and not draw anything else.

The same approach applies to some animations. **If the browser is asked to perform a transform animation for some element, the browser renders this element on a separate layer and during the animation, instead of repainting, it will recompose the already drawn layers. Composition happens on the GPU, so it's very fast.**

Animating the left/top position of an element happens by drawing each new frame. Therefore, such animation requires more resources.

If you are using complex styles such as box-shadow, calculating the new coordinates and styles of an element and rendering its new state may not be within 16 ms - the time it takes for a frame to be drawn to produce 60 frames per second. In this case, your users will see the animation isn't smooth.

See demo.

## 📄 Reference

> https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/

> https://web.dev/i18n/ko/fcp/

> https://choi95.tistory.com/166
