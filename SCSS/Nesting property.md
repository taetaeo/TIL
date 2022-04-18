# Nesting property (중첩된 속성)

<br/>

## scss 중첩된 속성

#### # scss

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
    padding{
        top:10px;
        bottom:40px;
        left:20px;
        right:30px;
    }
}
```

#### # css

```css
.box {
  font-weight: bold;
  font-size: 10px;
  font-family: sans-serif;
  margin-top: 10px;
  margin-left: 20px;
}
.box padding {
  top: 10px;
  bottom: 40px;
  left: 20px;
  right: 30px;
}
```

- `:` 기호로 시작하여 중첩된 속성을 나타낼 수 있습니다.

- `font: {};` 와 같이 font의 font-weight, font-size, font-family 등의 여러가지 속성을 중첩하여 표현이 가능합니다.
- 이렇게 `font-` 로 시작하여 폰트를 나타내는 속성들을 `"네임스페이스가 동일하다"`라고 합니다. 
- 네임스페이스란 이름을 통해 구분 가능한 범위를 만들어내는 것으로 일종의 유효범위를 지정하는 방법을 말합니다.
- 또한, 주의할 사항은 반드시 중괄호가 끝나는 부분에는 `;`을 표시해주어야 합니다. 아래에 예를 살펴봅시다.

