# Parent Selector(부모 선택자)

<br/>

## 부모 선택자(상위 선택자)

- 상위 선택자 참조는 `&` 를 사용한다.
- 부모 선택자는 특수문자 '**&**'을 사용한다.
- 기본적으로 **중첩**된 Sass 문법 **안에**서 사용한다.
- \- :hover, :checked, :not(&) 등의 **가상클래스**에 사용된다.
- :after, :before 등의 **가상요소**에 사용된다.
- 언더바(_), 하이픈(-) 등의 클래스명의 **접속사**에 사용한다.

#### # scss

```scss
.btn{
    position:absolute;
    &.active{
        color:red;
    }
}

.list{
    li{
        &:last-chlid{
            margin-right:0;
        }
    }
}
```

#### # css

```css
.btn {
  position: absolute;
}
.btn.active {
  color: red;
}

.list li:last-chlid {
  margin-right: 0;
}
```

- `.btn` 의 결과로 `&` 영역에 치환됐다. 즉, `&`는 상위 선택자를 참조하는 기능을 한다.

- `.list` 의 결과로, `&` 는 가상클래스 선택자에 참조한다. 즉, `&`는 `<li>` 태그를 의미한다.
- `&` 는 자신이 포함된 상위 선택자를 참조하는 기능이다. (=상위 선택자가 `&` 기호로 하위 선택자에 치환이 된다.)

#### # scss

```scss
.fs{
    &-small{font-size:12px;}
    &-medium{font-size:14px;}
    &-large{font-size:16px;}
}
```

#### # css

```css
.fs-small {
  font-size: 12px;
}
.fs-medium {
  font-size: 14px;
}
.fs-large {
  font-size: 16px;
}
```

- `&` 기호는 자신이 포함된 영역의 그 선택자를 참조한다.
  - 즉, 상위선택자를 참조한다.