# 13. 참조형 State

- `배열`이나 `객체`같은 참조형 State를 다룰 때 주의해야할 점

<br/>

## 13.1. sum State

### 13.1.1. 총점을 계산하는 State 구현하기

#### 1) App.js

```react
import { useState } from "react";
import Button from "./Button";
import Dice from "./Dice";

function random(n) {
  return Math.ceil(Math.random() * n);
}

function App() {
  const [num, setNum] = useState(1);
  // 1. sum State
  const [sum, setSum] = useState(0)

  const handleRollClick = () => {
    const nextNum = random(6);
    setNum(nextNum);
    setSum(sum+nextNum); // 2.
  };

  const handleClearClick = () => {
    setNum(1);
    setSum(0)
    
  };
  return (
    <div>
      <div>
        <Button onClick={handleRollClick}>던지기</Button>
        <Button onClick={handleClearClick}>처음부터</Button>
      </div>
      <div>
        <h2>나</h2>
        <Dice color="red" num={num} />
        <h2>총점</h2>
        <p>{sum}</p>
      </div>
    </div>
  );
}

export default App;

```

1. `sum` State를 만들어준다. 초기값은 숫자 0으로 한다. 그리고, 버튼을 클릭할 때마다 주사위 값을 더해줘야 한다.
2. State값을 변경하기 위해서는, setSum인 setter함수를 이용해준다.
   - `setNum` 함수를 호출해주고, Argument로 sum State와, nextNum을 더해준다.
   - 던지기 버튼을 누를때마다, 새로운 주사위 숫자값이 `sum` State에 더해진다.

3. 초기화 버튼을 누를때, 숫자값이 0으로 하기 위해서, `setSum(0)`을 호출한다.

4. JSX에 `{sum}`을 호출하도록 한다.

<br/>

## 13.2. 기록 State

- 기록에는 그동안 나온 주사위 숫자값들을 하나씩 모아서 보여준다.
- 순서대로 하나씩 기록하므로, `배열(array)`로 만들어준다.

<br/>

### 13.2.1. 배열 State (1)

#### 1) App.js

```react
function App() {
  const [num, setNum] = useState(1);
  const [sum, setSum] = useState(0);
  // 1. 배열 State
  const [gameHistory, setGameHistory] = useState([]);

  const handleRollClick = () => {
    const nextNum = random(6);
    setNum(nextNum);
    // 2. 주사위 값 추가
    gameHistory.push(nextNum)
    setGameHistory(gameHistory)
  };

  const handleClearClick = () => {
    setNum(1);
    setSum(sum + nextNum);
    // 3. 초기화 기능
    setGameHistory([])
  };
  return (
    <div>
      <div>
        <Button onClick={handleRollClick}>던지기</Button>
        <Button onClick={handleClearClick}>처음부터</Button>
      </div>
      <div>
        <h2>나</h2>
        <Dice color="red" num={num} />
        <h2>총점</h2>
        <p>{sum}</p>
      </div>
    </div>
  );
}
```

1. `[]` 빈 배열을 초기값으로 받는 `gameHistory` State를 만들어주고, 새로 던져서 나온 주사위 값을 추가해도록 한다.
2. `gameHistory.push(nextNum)`  = 배열 State에 주사위값을 넣어주고, setter함수(`setGameHistory` )에 추가된 `gameHistory`  State 값을 넣어준다.
3. `  setGameHistory([])` = 초기값이 빈 배열의 형태를 전달해주어, 초기화 상태를 지정하도록 한다.

<br/>

#### 하지만, 이렇게하면 잘못되었다.

- 배열은 기본형이 아니라, 참조형이다. 
- `gameHistory` 변수는 기록들을 가진 배열 자체의 값을 갖는게 아니라, 그 배열을 가리키고 있는 주소값을 가지고 있는 것이다. 
- 그렇기 때문에, 메소드를 이용해 배열에 새로운 요소를 집어 넣어도 `gameHistory` 가 가지고있는 배열의 주소값은 변하지 않는다.

- 따라서, `배열` 이나 `객체`같은 참조형 타입의 State를 변경해야할 때는 전체를 새로 만든다고 생각하는 것이 좋다. 
  - 그 방법중에 하나는 `...` 스프레드 문법을 사용하는 것이다. 

<br/>

### 13.2.2. 배열 State (2)

#### 1) App.js

```react
function App() {
  const [num, setNum] = useState(1);
  const [sum, setSum] = useState(0);
  const [gameHistory, setGameHistory] = useState([]);
  // State 변경
  const handleRollClick = () => {
    const nextNum = random(6);
    setNum(nextNum);
    setSum(sum + nextNum);
    // 1.
    setGameHistory([...gameHistory,nextNum]);

  };
  // 초기화 기능
  const handleClearClick = () => {
    setNum(1);
    setSum(sum + nextNum);
    setGameHistory([])
  };
  return (
    <div>
      <div>
        <Button onClick={handleRollClick}>던지기</Button>
        <Button onClick={handleClearClick}>처음부터</Button>
      </div>
      <div>
        <h2>나</h2>
        <Dice color="red" num={num} />
        <h2>총점</h2>
        <p>{sum}</p>
      </div>
    </div>
  );
}
```

1. `  setGameHistory([...gameHistory,nextNum]);`  
   - 빈 배열 안에, `gameHistory` State를 펼쳐주고, 그다음에 새로 추가할 요소(`nextNum`)를 붙여준다.

- 그다음 불필요한 코드들은 지운다.



- 위 코드에서 첫 번째 변수는 원하는 `state`의 이름(`num`)을 지어주고, 두 번째 변수에는 `state` 이름앞에 `set`을 붙인 다음 카멜 케이스로 이름을 지어주는 것이 일반적이다.
  - `setNum`
- `state`는 변수에 새로운 값을 할당하는 방식으로 변경하는 것이 아니라 이 `setter` 함수를 활용해야 한다.
- `setter` 함수는 호출할 때 전달하는 아규먼트 값으로 `state`값을 변경해준다.
- 그래서 아래 코드처럼 `setter` 함수를 활용해서 이벤트 핸들러를 등록해두면, 이벤트가 발생할 때마다 상태가 변하면서 화면이 새로 그려진다.

<br/>

## 13.3. 정리하기

- `배열`이나 `객체`같은 참조형 State를 사용할 때는 메소드나 할당연산자로 값을 바꾸는 것이 아니라, 반드시 새로운 값을 만들어서, 변경해야한다.
- 그 방법 중 하나가 `스프레드 문법`을 사용하는 것이다. = `...`

<br/>

## 13.4. 완성 코드

#### 1) App.js

```react
import { useState } from "react";
import Button from "./Button";
import Dice from "./Dice";

function random(n) {
  return Math.ceil(Math.random() * n);
}

function App() {
  const [num, setNum] = useState(1);
  const [sum, setSum] = useState(0);
  const [gameHistory, setGameHistory] = useState([]);
  // State 변경
  const handleRollClick = () => {
    const nextNum = random(6);
    setNum(nextNum);
    setSum(sum + nextNum);
    setGameHistory([...gameHistory, nextNum]);
  };
  // 초기화 기능
  const handleClearClick = () => {
    setNum(1);
    setSum(0);
    setGameHistory([]);
  };
  return (
    <div>
      <div>
        <Button onClick={handleRollClick}>던지기</Button>
        <Button onClick={handleClearClick}>처음부터</Button>
      </div>
      <div>
        <h2>나</h2>
        <Dice color="red" num={num} />
        <h2>총점</h2>
        <p>{sum}</p>
        <h2>기록</h2>
        <p>{gameHistory.join(", ")}</p>
      </div>
    </div>
  );
}

export default App;

```

