# 재활용 @content

<br/>

## SCSS 재활용 @content

- SCSS에서는 `@mixin` 기호를 활용하여 특정한 이름에 내용을 저장하고 `@include` 키워드로 해당 내용을 재활용할 수 있었습니다.
- `@content`는 `@mixin` 내의 추가적으로 필요한 내용에 대해 담는 그릇으로 사용할 수 있습니다. `@include`로 호출하여 중괄호 내에 더해줄 추가적인 내용을 입력해주면 됩니다. 아래의 예시에서 알아봅시다.

<br/>

## `@content`

#### # scss

```scss
@mixin left-top {
    position: absolute;
    top: 0;
    left: 0;
    @content;
}

.container{
    width: 100px;
    height: 100px;
    @include left-top;
}

.box{
    width: 200px;
    height: 300px;
    @include left-top{
        bottom: 0;
        right: 0;
        margin: auto;
    }
}
```

#### # css

```css
.container {
  width: 100px;
  height: 100px;
  position: absolute;
  top: 0;
  left: 0;
}

.box {
  width: 200px;
  height: 300px;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
}
```

- `.box`의 경우, `left-top`에서  `@content`가 있으므로,   중괄호를 `{}` 통해서 추가적으로 내용을 넣을 수 있다.
- 일반적인 경우나 실무에서 유용하게 쓰이지는 않지만, `bootstrap` 같은 외부의 패키지를 사용할 때, 쓰일 수 있다. 

<br/>