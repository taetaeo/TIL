# variable 변수

<br/>

## scss 변수

- scss에서는 `$` 기호를 이용하여 JavaScript에서 사용하는 `const`, `let` 등과 마찬가지로 변수를 선언할 수 있습니다.
- 자바스크립트에서는 `const size = 100px;` 와 같은 방식이지만, scss에서는 다르다.
- `$size: 100px;`의 예처럼 앞에 `$`를 적고 할당 연산자로 `:`을 사용하는 방식으로 `size`라는 변수에 값을 입력합니다. 해당 변수는 SCSS 내에서 반복적으로 활용이 가능하기 때문에 자주 사용되는 기능입니다.

#### # scss

```scss
$size: 100px;

.constainer{
    position:fixed;
    top:$size;
    .item{
        width:$size;
        height:$size;
        transform:tarnslate($size);
    }
}

```

#### # css

```css
.constainer {
  position: fixed;
  top: 100px;
}
.constainer .item {
  width: 100px;
  height: 100px;
  transform: tarnslate(100px);
}
```

<br/>

## 변수 사용시 장점

- 변수를 사용할 시 장점으로, 재활용이 가능하며, 수정에 용이해진다.
- 따라서, 변수는 반복된 수치 혹은 주요하게 사용하는 main 색상 또는 크기 등에 변수를 부여한다.

<br/>

## 변수 사용시 주의 사항

- 유의해야할 점은 변수는 선언한 범위 내에서 유효 범위를 가집니다. 

- 전역 변수는 문제 없이 모두 활용이 가능하나 변수가 특정한 중괄호 내에서 사용이 된다면, 
- 해당 범위 내에서만 유효 범위를 가지므로 다른 곳에서는 활용이 불가합니다.
- 추가적으로 `let`과 동일하게 재할당이 가능합니다. 재할당된 변수는 `let`과 마찬가지로 이후 해당 유효 범위 아래에서 할당된 값으로 활용됩니다. 아래의 예시를 살펴봅시다.

즉, `$size:200px;` 로 지정한 변수같은 경우 전역에서 사용이 가능하다.  하지만, `$size2:100px;` 같은 경우에는 변수가 선언된 `{}` 안에서만 사용이 가능하다.

```scss
$size: 100px;

.constainer{
    $size2:100px;
    position:fixed;
    top:$size;
    .item{
        width:$size;
        height:$size;
        transform:tarnslate($size);
    }
}
.box{
    width:$size2; // 불가능하다.
}
```

<br/>

## 변수의 재할당

#### # scss

```scss

.constainer{
    $size:200px;
    position:fixed;
    top:$size;
    .item{
        $size:100px;
        width:$size;
        height:$size;
        transform:tarnslate($size);
    }
    left:$size;
}

```

#### # css

```css
.constainer {
  position: fixed;
  top: 200px;
  left: 100px;
}
.constainer .item {
  width: 100px;
  height: 100px;
  transform: tarnslate(100px);
}
```

- 200px이 아닌, 새롭게 정의한 100px이 입력된다.
- 또한, `left:$size;` 의 경우 200px이 아닌, 100px이 되었다.
- 재할당된 코드 아래쪽에서는 재할당된 값으로 출력이 된다.

- 따라서, scss에서의 변수 `$` 는 자바스크립트의  `let` 선택자와 비슷한 기능을 한다.

