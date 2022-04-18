# nesting (중첩)

<br/>

## 중첩 기능

#### # html

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

#### #scss

```scss
$color:royalblue;
.container{
  ul{
    li{
      font-size:40px;
      .name{
        color:$color;
      }
      .age{
        color:orange;
      }
    }
  }
}

```

#### # css

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
```

<br/>

## 자식 선택자 

- `<ul>` 태그 부분이 `<containter>`의 자식요소임을 표현하기 위해서는 `>` 을 활용한다.

```scss
$color:royalblue;
.container{
  > ul{
    li{
      font-size:40px;
      .name{
        color:$color;
      }
      .age{
        color:orange;
      }
    }
  }
}
```

