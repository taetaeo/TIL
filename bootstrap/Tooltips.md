# Tooltips

[Tooltips 더 알아보기](https://getbootstrap.com/docs/5.1/components/tooltips/)

- Tooltips rely on the 3rd party library [Popper](https://popper.js.org/) for positioning. You must include [popper.min.js](https://cdn.jsdelivr.net/npm/@popperjs/core@2.10.2/dist/umd/popper.min.js) before bootstrap.js or use `bootstrap.bundle.min.js` / `bootstrap.bundle.js` which contains Popper in order for tooltips to work!
- :star: Tooltips are opt-in for performance reasons, so **you must initialize them yourself**. :star:
  - Tooltips을 사용하기 위해서는 자바스크립트로 초기화를 해야한다.
- Tooltips with zero-length titles are never displayed.
- Specify `container: 'body'` to avoid rendering problems in more complex components (like our input groups, button groups, etc).
- Triggering tooltips on hidden elements will not work.
- Tooltips for `.disabled` or `disabled` elements must be triggered on a wrapper element.
- When triggered from hyperlinks that span multiple lines, tooltips will be centered. Use `white-space: nowrap;` on your `<a>`s to avoid this behavior.
- Tooltips must be hidden before their corresponding elements have been removed from the DOM.
- Tooltips can be triggered thanks to an element inside a shadow DOM.



## Tooltips 이란?

- 어떤 부분에 마우스를 올리면, 일종의 설명이 팝업이 나오는 것

```html
<button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="top" title="Tooltip on top">
    Tooltip on top
</button>
<button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="right" title="Tooltip on right">
    Tooltip on right
</button>
<button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="bottom" title="Tooltip on bottom">
    Tooltip on bottom
</button>
<button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="left" title="Tooltip on left">
    Tooltip on left
</button>
```

- 하지만 바로 작동하지 않기 때문에, JS코드로 초기화를 해야한다.

#### Tooltips.js

```js
var tooltipTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="tooltip"]'))
var tooltipList = tooltipTriggerList.map(function (tooltipTriggerEl) {
  return new bootstrap.Tooltip(tooltipTriggerEl)
})
```



