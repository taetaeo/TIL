# SCSS

## 목차

01. [개요]()
02. [프로젝트 생성]()
03. [주석](#3.-주석처리)
04. [중첩](#4.-중첩기능)
05. [상위(부모) 선택자 참조](#5.-상위(부모)-선택자-참조)
06. [중첩된 속성](#6.-중첩된-속성)
07. [변수](#7.-변수)
08. 산술 연산
09. 재활용
10. 반복문
11. 함수
12. 색상 내장 함수
13. 가져오기
14. 리팩토링
15. 데이터 종류
16. 반복문 @each
17. 재활용 @content

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

## 6. 중첩된 속성

#### 네임스페이스

- `네임스페이스` 란 이름을 통해 구분 가능한 범위를 만들어내는 것으로 일종의 유효범위를 지정하는 방법을 말한다.
    - ex. `font-weight` , `font-size` 등 `font-`이라는 네임스페이스를 갖는다.
```scss
.box{
  font:{
    weight:bold;
    size:10px;
    family:sans-serif;
  };
  margin:{
    top:10px;
    left:20px;
  };
  padding:{
    top:10px;
    bottom:40px;
    left:20px;
    right:30px;
  };
}
```

```css
.box {
  font-weight: bold;
  font-size: 10px;
  font-family: sans-serif;
  margin-top: 10px;
  margin-left: 20px;
  padding-top: 10px;
  padding-bottom: 40px;
  padding-left: 20px;
  padding-right: 30px;
}

```

## 7. 변수

- 동일한 수치 또는 값이 반복되어 사용이 될 때, 변수를 사용한다.
- 변수를 사용할 때 주의 사항
    - 변수는 선언된 범위에서 유효범위를 갖는다.


### 7.1. 전역 변수

#### 7.1.1 변수 사용 - scss

```scss
$size : 100px; // 1. 전역 변수
.container {
  position:fixed;
  top:$size;
  .item{
    width: $size;
    height:$size;
    transform: translateX($size);
  }
}
```
#### 7.1.2 변수 컴파일 - css

```css
.container {
  position: fixed;
  top: size;
}
.container .item {
  width: size;
  height: size;
  transform: translateX(size);
}
```

### 7.2. 유효 범위가 아닐 때,

```scss
.container {
  $size : 100px;
  position:fixed;
  top:$size;
  .item{
    width: $size;
    height:$size;
    transform: translateX($size);
  }
}
.box{
  width: $size;
}//  에러가 발생한다.
```
- `$size` 변수는 `.container` 안에서만 변수를 지정을 했으므로,
- 변수의 유효 범위를 벗어나 에러가 발생한다.

```css
.container {
  position: fixed;
  top: 100px;
}
.container .item {
  width: 100px;
  height: 100px;
  transform: translateX(100px); 
}
```

### 7.3. 변수 재할당

```scss
.container {
  $size : 200px;
  position:fixed;
  top:$size;
  .item{
    $size: 100px;
    width: $size;
    height:$size;
    transform: translateX($size);
  }
}
```

```css
.container {
  position: fixed;
  top: 200px;
}
.container .item {
  width: 100px;
  height: 100px;
  transform: translateX(100px);
}
```
- `.item` 안에서 변수를 100px로 재할당 했으므로,
- 200px이 아닌, 100px의 값을 받게 된다.