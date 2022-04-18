# function

<br/>

## scss 함수

- SCSS에서 `@mixin`을 이용하여 함수와 유사하게 사용하는 방법도 있지만 실제로 `@function`을 SCSS 내에서 JavaScript 함수와 동일한 구조로 활용할 수 있습니다.
- 따라서, `@mixin`은 CSS의 style을 다루는 데에 주로 사용이 된다면, `@function`은 어떠한 값을 명시하는 데에 사용할 수 있다.
- `@function` 의 경우 매개변수와 `@return` 키워드를 통해 값을 반환하는 구조는 JavaScript와 유사하다.

#### # scss

```scss
// 재활용
@mixin center{
    display:flex;
    justify-content:center;
    align-items:cneter;
}

// 함수를 통해서 반환된 값을 활용
@function ratio($size, $ratio){
    @return $size * $ratio
}

.box{
    $width:100px;
    width:$width;
    height:ratio($width, 1/2);
    @include center
}
```

#### # css

```css
.box {
  width: 100px;
  /* @function */
  height: 50px; 
   /* @mixin */
  display: flex;
  justify-content: center;
  align-items: cneter;
}
```

- 또한, `@function` 의 경우 다른 부분에서 재활용이 될 수 있다.