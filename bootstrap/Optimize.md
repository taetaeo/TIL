# 성능 최적화(트리 쉐이킹)

<br/>

# Optimize

[Optimize 더 알아보기](https://getbootstrap.com/docs/5.1/customize/optimize/)

- 부스트스트랩에서 필요로하는 기능만 가지고 와서 쓸 수 있다.

### Lean Sass imports

- 최대한 간결하고 군더더기 없이 scss의 기능을 가져와서 사용할 수 있다.

```scss
// Configuration
@import "functions";
@import "variables";
@import "mixins";
@import "utilities";

// Layout & components
@import "root";
@import "reboot";
@import "type";
@import "images";
@import "containers";
@import "grid";
@import "tables";
@import "forms";
@import "buttons";
@import "transitions";
@import "dropdown";
@import "button-group";
@import "nav";
@import "navbar";
@import "card";
@import "accordion";
@import "breadcrumb";
@import "pagination";
@import "badge";
@import "alert";
@import "progress";
@import "list-group";
@import "close";
@import "toasts";
@import "modal";
@import "tooltip";
@import "popover";
@import "carousel";
@import "spinners";
@import "offcanvas";
@import "placeholders";

// Helpers
@import "helpers";

// Utilities
@import "utilities/api";
```

<br/>

### Lean JavaScript

```js
// Import just what we need

// import 'bootstrap/js/dist/alert';
// import 'bootstrap/js/dist/button';
// import 'bootstrap/js/dist/carousel';
// import 'bootstrap/js/dist/collapse';
// import 'bootstrap/js/dist/dropdown';
import 'bootstrap/js/dist/modal';
// import 'bootstrap/js/dist/offcanvas';
// import 'bootstrap/js/dist/popover';
// import 'bootstrap/js/dist/scrollspy';
// import 'bootstrap/js/dist/tab';
// import 'bootstrap/js/dist/toast';
// import 'bootstrap/js/dist/tooltip';
```

- 대신에 가지고 올 때는, 기본적인 초기화 과정을 거쳐야 한다.

> **Default Exports** (기본 내보내기)
>
> ``` js
> import Modal from 'bootstrap/js/dist/modal'
> 
> const modal = new Modal(document.getElementById('myModal'))
> ```
>
> - 기본 내보내기 방식으로 받아서 사용할 수 있고,
> - `new` 라는 키워드와 함께 생성자 키워드와 함께 사용



