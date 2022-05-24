# 11. State

- 컴포넌트에서 동적인 값을 상태(state)라고 부릅니다. 리액트에 `useState` 라는 함수가 있다.
- 이것을 사용하면 컴포넌트에서 상태를 관리 할 수 있습니다.

<br/>

## 11.1. State가 왜 필요한가?

> `던지기 `버튼으로 주사위 던지는 기능을 구현할 떄,

- 주사위를 던지는 기능을 만들 때, `던지기` 버튼을 누르면, 주사위의 숫자가 바뀌면서, `HTML` 요소가 바뀌는 기능을 구현해야한다.
- 만약, 리액트없이 `HTML` 요소로만 구현을 한다면, 주사위마다 HTML 페이지를 만들고 이동시키거나, 자바스크립트로 HTML요소노드의 속성만 바꾸면서 구현한다.
- 그러나, 리액트에서는 이런 경우 사용하는 핵심 기능이 있는데, 그것이 `State` 이다.

<br/>

> 리액트에서`State` 

- `State`는 리액트에서 변수같은 것인데, `state`를 바꾸면, 리액트가 알아서 화면을 새로 `랜더링`하는 것이다. 

<br/>

## 11.2. State정의

- `State`는 리액트에서 화면을 그려내는데 중요한 역할을 한다.
- `State`라는 단어는 '상태'라는 뜻이다. 리액트에서의 `State`도 그 의미가 다르지 않다.
- 상태가 바뀔 때마다 화면을 새롭게 그려내는 방식으로 동작을 하는 것이다.
- 리액트에서 `State`를 만들고, `State`를 바꾸기 위해서는 일단 `useState` 함수를 사용해야 한다.

<br/>

### 11.2.1. State 사용방법

```react
import { useState } from 'react';

// ...

  const [num, setNum] = useState(1);

// ...
```

- 보통 이렇게 배열의 `Destructuring` 문법으로 작성한다.  
- `useState` 함수는 파라미터로 초깃값을 전달 받고, =`1` , 그에 따른 실행 결과로 요소 2개를 가진 배열의 형태로 리턴을 한다.
- 이때, 첫 번째 요소가 바로 `state`이다. 
  - 즉, `현재 변수의 값`을 나타낸다. 
    - `useState(1)` 에서 호출한 `1` 을 가지고 있다.

- 두 번째 요소가 이 `state`를 바꾸는 `setter` 함수이다.
  - 이 함수를 호출할 때, 파라미터로 전달하는 값으로 `state`가 변경이 된다. 

<br/>

## 11.3. State 적용

### 11.3.1. `던지기` 버튼 기능

#### 1) App.js

```react
import { useState } from "react";
import Button from "./Button";
import Dice from "./Dice";

function App() {
  // 1. num State
  const [num, setNum] = useState(1);
    
  return (
    <div>
      <div>
        <Button>던지기</Button>
        <Button>처음부터</Button>
      </div>
      <Dice color="red" num={num} />
    </div>
  );
}
export default App;
```

1. `num` State를 만들었으니, `num` State를 `<Dice />` 컴포넌트의 `num` Prop으로 내려준다.
   - `<Dice color="red" num={num} />`

<br/>

````react
import { useState } from "react";
import Button from "./Button";
import Dice from "./Dice";

function App() {
  const [num, setNum] = useState(1);
  
 // 2. 이벤트 핸들러
  const handleRollClick = () =>{
      setNum(3);
  }
  return (
    <div>
      <div>
        <Button onClick={handleRollClick}>던지기</Button>
        <Button>처음부터</Button>
      </div>
      <Dice color="red" num={num} />
    </div>
  );
}
export default App;
````

2. `num` State를 3으로 바꾸는, ` handleRollClick`이라는 함수를 만들고, 이 함수를 `던지기` 컴포넌트의 `onClick` Prop으로 내려준다.

3. 아직 버튼 컴포넌트에는 `onClick` Prop에 대한 처리가 없으므로, `Button.js` 컴포넌트에 가서 적용한다.

<br/>

#### 2) Button.js

```react
function Button({ children, onClick }) {
  return <button onClick={onClick}>{children}</button>;
}
export default Button;
```

4. 파라미터로 ` onClick ` Prop을 받고, `onClick` 이벤트에 `onClick Prop`을 내려준다.

<br/>

### 11.3.2. Random하게 숫자를 변경하는 기능

#### 1) App.js

```react
import { useState } from "react";
import Button from "./Button";
import Dice from "./Dice";

// 1. random 숫자 불러오기
function random(n){
    return Math.ceil(Math.random()*n)
}
function App() {
  const [num, setNum] = useState(1);
  
  const handleRollClick = () =>{
      const nextNum = random(6)
      setNum(nextNum);
  }
  return (
    <div>
      <div>
        <Button onClick={handleRollClick}>던지기</Button>
        <Button>처음부터</Button>
      </div>
      <Dice color="red" num={num} />
    </div>
  );
}
export default App;
```

1. `random`한 숫자를 불러 올 수 있는 함수를 만들고, 이 함수는 파라미터 `n`으로 숫자값을 전달받아서,  1부터 n까지의 랜덤한 정수를 반환한다.
   - 따라서, 6을 넣어주면, 1부터 6까지의 랜덤한 정수를 반환한다.
2. `handleRollClick`에 적용한다. `const nextNum = random(6)` 으로, 랜덤한 정수를 `nextNum`이라는 변수에 할당하고, 그 값으로,  `setNum(nextNum);` 즉, num의 setter함수에 적용하여 num State를 변경한다.

<br/>

### 11.3.3. `처음부터` 버튼 - 초기화 기능

#### 1) App.js

```react
import { useState } from "react";
import Button from "./Button";
import Dice from "./Dice";

function random(n){
    return Math.ceil(Math.random()*n)
}
function App() {
  const [num, setNum] = useState(1);
  
  const handleRollClick = () =>{
      const nextNum = random(6)
      setNum(nextNum);
  }
  // 1. handleClearClick 함수 - 초기화기능
  const handleClearClick = () =>{
      setNum(1)
  }
  return (
    <div>
      <div>
        <Button onClick={handleRollClick}>던지기</Button>
        <Button onClick={handleClearClick}>처음부터</Button>
      </div>
      <Dice color="red" num={num} />
    </div>
  );
}
export default App;
```

1. `handleClearClick` 함수를 만들어서, num의 `setter`함수에 1을 넣어주면, num State가 1로 변경이 된다. 
2. 그리고 `<button />` 컴포넌트의 `onClick` Prop으로 내려준다.

<br/>

## 11.4. 정리

- 리액트의 `State` 기능에 대해서 알아보았다.  `State` 는 리액트에서 화면을 변경할 때, 활용하는 핵심적인 기능이다. 

- 왜냐하면, 리액트에서는  `State` 값이 변경이 될 때마다 화면을 새롭게 랜더링한다.
- 컴포넌트에서  `State` 를 사용하려면, `useState` 함수를 불러와야한다.
- 그리고 그 함수는  `State` 와 `setter` 함수를 배열의 형태로 리턴한다.
- 따라서, 배열구조분해형태로 작성한다.
- 또한,  `State` 를 변경할 때는, 직접 변경하는 것이 아니라, `setter` 함수를 통해서 변경을 해야 한다.