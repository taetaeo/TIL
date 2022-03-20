# SCSS

## 참고 사이트

- sassmeiseter - [더 알아보기](https://www.sassmeister.com/)
    - 어떻게 scss코드가 변환이 되는지 확인할 수 있다.
    
## 2. SCSS 사용 - 변수

- `$`기호와 함께 변수를 할당할 수 있다.
```scss
$color:royalblue;

.container{
  h1 {
    color:$color;
    background-color: orange; /* */
    font-size: 60px;
  }
}
```
## 3. 주석처리

- `//` 의 경우에 SCSS에서 CSS로 변화할 때 `compile`이 되지 않는다.
- 하지만, `/**/` 의 경우에는 CSS로 변환할 때, `compile`이 되어 진다.

## 4. 중첩기능

#### 1) HTML 작성
```html
<div class="container">
  <ul>
    <li>
      <div class="name">HEROPY</div>
      <div class="age">85</div>
    </li>
  </ul>
</div>
```
#### 2) SCSS 작성
```scss
.container{
  ul {
    li{
      font-size: 40px;
      .name{
        color:royalblue
      }
      .age{
        color:orange
      }
    }
  }
}
```
#### 3) CSS compile 

```css
.container ul li {
  font-size: 40px;
}
.container ul li .name {
  color: royalblue;
}
.container ul li .age {
  color: orange;
}
/*# sourceMappingURL=/main.39afc03c.css.map */

```

## 5. 상위(부모) 선택자 참조

- `&` 기호는 자신이 포함된 영역의 그 선택자를 참조한다.
    - 즉, 상위선택자를 참조한다.

#### `&` 예시 1. SCSS
```scss
.btn{
  position: absolute;
  &.active{
    color:red
  }
}

.list{
  li{
    &:last-child{
      margin-right:0
    }
  }
}
```
#### `&` 예시 1. CSS
```css
.btn {
  position: absolute;
}
.btn.active {
  color: red;
}

.list li:last-child {
  margin-right: 0;
}
```

#### `&` 예시 2. SCSS

```scss
.fs{
  &-samll{font-size:12px;}
  &-medium{font-size:14px;}
  &-large{font-size: 16px;}
}
```

#### `&` 예시 2. CSS

```css
.fs-samll {
  font-size: 12px;
}
.fs-medium {
  font-size: 14px;
}
.fs-large {
  font-size: 16px;
}
```

## 6. 