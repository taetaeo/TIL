# Mixins (재활용)

<br/>

## scss 재활용

- SCSS에서는 `@mixin` 기호를 활용하여 특정한 이름에 내용을 저장하고 `@include` 키워드로 해당 내용을 재활용할 수 있습니다.

- 또한, `$` 기호를 활용한 변수를 매개변수와 인수로 넣어줌으로 재활용 기능을 사용하면서도 들어가 있는 내용을 수정하면서 사용할 수 있습니다. 
- `e.g. box($size)` 이는 JavaScript의 함수를 선언하고 호출하는 방식과 유사하다고 볼 수 있습니다.

#### # scss

```scss
@mixin center{
    display:flex;
    justify-content:cneter;
    align-items:center;
}

.container{
    @include center;
    .item{
        @include center
    }
}
.box{
    @include center
}

```

#### # css(compiled)

```css
.container {
  display: flex;
  justify-content: cneter;
  align-items: center; 
}
.container .item {
  display: flex;
  justify-content: cneter;
  align-items: center;
}

.box {
  display: flex;
  justify-content: cneter;
  align-items: center;
}
```

<br/>

### mixin에서 다른 값을 제공하고 싶다면?

- 자바스크립트와 마찬가지로 `인수`와 `매개변수`라는 것을 사용하게 된다.

#### # scss

```scss
@mixin box($size){
    width:$size;
    height:$size;
    background-color:tomato;
}
.container {
    @include box(200px);
    .item{
        @include box(100px);
    }
}

.box{
    @include box(100px);
}
```

#### # css

```css
.container {
  width: 200px;
  height: 200px;
  background-color: tomato;
}
.container .item {
  width: 100px;
  height: 100px;
  background-color: tomato;
}

.box {
  width: 100px;
  height: 100px;
  background-color: tomato;
}
```

- 여기서 `box(data)`의 코드에서 `data`는 인수에 해당하고, `@mixin box($size)` 에서 `$size`는 매개변수에 해당한다.

<br/>

### mixin의 매개변수에 기본값을 지정하기

#### # scss

```scss
@mixin box($size:100px){ // 기본값 지정
    width:$size;
    height:$size;
    background-color:tomato;
}
.container {
    @include box(200px);
    .item{
        @include box;
    }
}

.box{
    @include box;
}
```

- `box($size:100px)` 처럼, 인수를 넣지 않을때, 기본값 100px이 할당된다.

#### # css

```css
.container {
  width: 200px;
  height: 200px;
  background-color: tomato;
}
.container .item {
  width: 100px;
  height: 100px;
  background-color: tomato;
}

.box {
  width: 100px;
  height: 100px;
  background-color: tomato;
}
```

<br/>

### 매개변수를 여러개 사용하기

#### # scss

```scss
@mixin box($size:100px, $color:tomato){
    width:$size;
    height:$size;
    background-color:$color;
}
.container {
    @include box(200px,royalblue);
    .item{
        @include box(100px, green); // 인수를 넣는 순서 주의
    }
}

.box{
    @include box;
}
```

-  `@include box(100px, green);` 처럼 인수를 넣는 순서에 주의해야한다.
- 이러한 불편을 줄이기 위해서 `키워드 인수`를 사용한다.

#### # css

```css
.container {
  width: 200px;
  height: 200px;
  background-color: royalblue;
}
.container .item {
  width: 100px;
  height: 100px;
  background-color: green;
}

.box {
  width: 100px;
  height: 100px;
  background-color: tomato;
}
```

<br/>

### 키워드 인수

#### # scss

```scss
@mixin box($size:100px, $color:tomato){
    width:$size;
    height:$size;
    background-color:$color;
}
.container {
    @include box(200px,royalblue);
    .item{
        @include box($color: green);
    }
}

.box{
    @include box;
}
```

-  `@include box($color: green)` 해당하는 값이 해당 인수에 직접적으로 값이 들어가게 된다.
- 이렇게 하면 순서와 상관없이 입력할 수 있게 된다. 

#### # css

```css
.container {
  width: 200px;
  height: 200px;
  background-color: royalblue;
}
.container .item {
  width: 100px;
  height: 100px;
  background-color: green;
}

.box {
  width: 100px;
  height: 100px;
  background-color: tomato;
}
```

