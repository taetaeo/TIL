# 반복문 @each

<br/>

## SCSS 반복문 @each

- 이번에는 JavaScript의 배열과 유사한 `$list`와 객체의 개념인 `$map`을 이용하여 SCSS에서 `each` 키워드를 통해 반복문을 구현해내는 방법을 알아봅시다.

<br/>

## `@each (변수) in (리스트Data)`

#### # scss

```scss
$number:1; // .5, 100px, 1em
$string:bold; // realative, "../images/a.png"
$color:red; // blue, #FFFF00, rgba(0,0,0, .1)
$boolean:true; // false
$null:null;
$list: orange, royalblue, yellow;
$map: (
    o:orange,
    r:royalblue,
    y:yellow
    );
    
@each $c in $list {
    .box{
        color:$c;
    }
}
```

#### # css

```css
.box {
  color: orange;
}

.box {
  color: royalblue;
}

.box {
  color: yellow;
}
```

<br/>

## `@each (변수) in (mapData)`

#### # scss

```scss
$number:1; // .5, 100px, 1em
$string:bold; // realative, "../images/a.png"
$color:red; // blue, #FFFF00, rgba(0,0,0, .1)
$boolean:true; // false
$null:null;
$list: orange, royalblue, yellow;
$map: (
    o:orange,
    r:royalblue,
    y:yellow
    );
    
@each $k, $v in $map {
    .box-#{$k}{
        color:$v;
    }
}
```

#### # css

```css
.box-o {
  color: orange;
}

.box-r {
  color: royalblue;
}

.box-y {
  color: yellow;
}
```

