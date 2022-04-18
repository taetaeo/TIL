# scss annotation

<br/>

# scss annotation & css

\- `//` 의 경우에 SCSS에서 CSS로 변화할 때 `compiled`이 되지 않는다.

\- 하지만, `/**/` 의 경우에는 CSS로 변환할 때, `compiled`이 되어 진다.

#### # scss (uncompile)

```scss
$color:royalblue;
.container{
  h1{
  color:$color;
  /* background-color:orange;*/
  // font-size:60px;
  }
}
```

#### # css (compiled)

```css
.container h1 {
  color: royalblue;
  /* background-color:orange;*/
}
```

- `//` 주석은 변환이 되지 않음.