# Button Group

[button Group 더 알아보기](https://getbootstrap.com/docs/5.1/components/button-group/)

```html
<div class="btn-group" role="group" aria-label="Basic example">
  <button type="button" class="btn btn-primary">Left</button>
  <button type="button" class="btn btn-primary">Middle</button>
  <button type="button" class="btn btn-primary">Right</button>
</div>
```

- `btn-group`  클래스 안에 감싸줌으로써 group화를 시켜 UI를 제공해줄 수 있다.

## Outlined styles

```HTML
<div class="btn-group" role="group" aria-label="Basic outlined example">
  <button type="button" class="btn btn-outline-primary">Left</button>
  <button type="button" class="btn btn-outline-primary">Middle</button>
  <button type="button" class="btn btn-outline-primary">Right</button>
</div>
```

- `btn-outline-primary` btn-primary 사이에 outline을 추가함으로써 테두리만 남은 버튼의 UI를 구현

## Sizing

```html
<div class="btn-group btn-group-lg" role="group" aria-label="...">...</div>
<div class="btn-group" role="group" aria-label="...">...</div>
<div class="btn-group btn-group-sm" role="group" aria-label="...">...</div>
```

- `bg-lg` , `bg-sm` 등을 통해서 button의 크기를 조절할 수 있다. 

## Nesting

```html
<div class="btn-group" role="group" aria-label="Button group with nested dropdown">
  <button type="button" class="btn btn-primary">1</button>
  <button type="button" class="btn btn-primary">2</button>

  <div class="btn-group" role="group">
    <button id="btnGroupDrop1" type="button" class="btn btn-primary dropdown-toggle" data-bs-toggle="dropdown" aria-expanded="false">
      Dropdown
    </button>
    <ul class="dropdown-menu" aria-labelledby="btnGroupDrop1">
      <li><a class="dropdown-item" href="#">Dropdown link</a></li>
      <li><a class="dropdown-item" href="#">Dropdown link</a></li>
    </ul>
  </div>
</div>
```

## Vertical variation

```html
<div class="btn-group-vertical">
  ...
</div>
```

- `btn-group` 에 `vertical` 요소를 넣음으로써, 수직형태의 버튼의 UI를 구성
