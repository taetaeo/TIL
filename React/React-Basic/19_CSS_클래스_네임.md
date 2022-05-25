# 19. CSS 클래스 네임

- `CSS` 클래스를 사용해서 컴포넌트의 디자인을 입힌다.

<br/>

## 19.1. css파일 불러오기

- 자바스크립트 파일에서 `css` 파일을 불러와서 적용한다.

<br/>

### 19.1.1. js 에서 css를 import

#### 1-1) index - js

```react
import ReactDOM from "react-dom/client";
import App from "./App";
// 1. css import
import "./index.css";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);

```

- 기존의 js를 import 하는 것과 유사하지만, 한가지 다른 점은 다음에 바로 파일 경로를 붙여주는 것이다.

<br/>

#### 1-1) index - css

```css
body{
  background-color: #191f2c;
  color:#fff;
}
```

<br/>

### 19.1.2. Button 컴포넌트 - CSS

#### 1) Button.css

```css
```





```react
```

