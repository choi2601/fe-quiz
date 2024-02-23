# Q72. Arrange the elements in ascending order of the amount of memory they occupy?

## ❓ Question

```css
.green {
  width: 50px;
  height: 50px;
  position: absolute;
  background: green;
}
.blue {
  width: 50px;
  height: 50px;
  position: fixed;
  background: blue;
}
.red {
  width: 1px;
  height: 1px;
  transform: scale(50);
  position: fixed;
  background: red;
}
```

- [] `green, blue, red`
- [] `green, red, blue`
- [] `blue, red, green`
- [x] `red, blue, green`

## 🤔 My Thinking

웹 페이지의 렌더링 과정은 크게 다음과 같다.

1. 레이아웃(Layout): 각 요소의 정확한 위치와 크기를 계산한다. 페이지의 구조가 어떻게 되어있는지, 각 요소가 화면상에서 어디에 위치해야 하는지 결정한다. 만약 요소의 크기나 위치가 변경되면, 레이아웃 단계가 다시 발생할 수 있다.
2. 페인트(Paint): 레이아웃 단계에서 결정된 요소들의 위치와 크기에 따라 실제로 화면에 그려지는 과정이다. 여기에는 텍스트 색상, 배경, 보더 등 시각적 스타일이 적용된다. 요소들이 어떻게 보여질지 결정하는 과정이며, 실제 픽셀로 변환되는 단계이다.
3. 합성(composition): 여러 레이어를 합쳐서 최종 이미지를 만드는 단계이다. 이 과정에서 브라우저는 다양한 레이어(예를 들어, 페이지 상단에 고정된 메뉴나 다른 요소들을 별도의 레이어로 처리할 수 있다)를 합쳐서 최종적으로 사용자에게 보여지는 페이지를 구성한다. 합성 단계는 GPU 가속을 사용할 수 있는 작업들(CSS `transform` 또는 `opacity` 변환)이
   해당 단계에서 처리된다.

`transform: scale`과 같은 CSS transform 속성은 렌더링 과정에서 특별한 처리를 받는다.

이 속성은 기존의 레이아웃 계산(원본 요소의 레이아웃이나 공간 배치)에 영향을 주지 않고, 합성(Compositing) 단계에서 적용된다.

1. 레이아웃(Layout): 여기서는 transform 속성이 적용되기 전의 원래 크기와 위치를 기반으로 계산이 이루어진다. 즉, `transform: scale`이 적용되어도 이 단계에서 요소의 원래 크기와 위치는 변하지 않는다.
2. 페인트(Paint): 이 때도 transform 속성의 영향은 받지 않는다.
3. 합성(Compositing): transform 속성은 이 단계에서 적용되어, 요소가 확대, 축소, 회전 등의 변화를 겪으며 최종적으로 사용자에게 보여지게 된다. 이 과정은 GPU를 통해 처리될 수 있어 성능이 우수하고, 원본 레이아웃에 영향을 주지 않으면서 시각적 변화를 제공한다.

## 🤓 Answer

Explanation.

When rendering a page, the browser splits it into layers, rasterizes each layer
(translates html and css data into pixels) separately, and sends the resulting images to the GPU, where they are stored. When the page needs to be rendered (when loading, scrolling, changing the DOM, etc.), the browser composes the layers into one.

The more layers and the larger the size of each layer, the more memory will be occupied.

The element with the green class has position: absolute. By default, elements with position: absolute are not rendered on a separate layer and do not take up any additional memory.

The red and blue elements have position: fixed. Since such elements are not tied to the background and should be in the same position when scrolling, the browser renders them on a separate layer.

The larger the element, the larger its layer and the more memory it takes.

Although we see the blue and red elements of the same size, they take up a different amount of memory. The browser stores the image before applying the transform: scale property and will only apply it at the time of actual rendering, so the layer of this element will be smaller and take up less memory.

Try this trick when memory is critical for you.

To see the different layer sizes of the blue and red elements:

go to dev tools -> Rendering -> Layer borders

https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/
