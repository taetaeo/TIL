# 9. Props

- 컴포넌트에 속성을 지정하는 방법

<br/>

## 9.1. Props란?

- 리액트에서 JSX문법으로 HTML 태그를 작성할 때 속성을 지정할 수 있고, 만약 이 속성에 자바스크립트 코드가 필요하다면, `{}`를 활용하면 되는데, 
- HTML 태그 뿐만아니라, 리액트 컴포넌트에도, 속성을 다양하게 지정할 수 있다. 
- 리액트에서는 컴포넌트에 지정한 속성을 `Props`라 한다.
- `Props` 란 프로퍼티스의 약어이다. 
- `Props`는 컴포넌트에 전달된 속성을 모두 가리키기 떄문에, 각각의 속성을 `prop`이라고 부른다.

<br/>

### 9.1.1. `Props` 활용 (1)

#### 1) Dice.js

```react
import diceBlue01 from "./assets/dice-blue-1.svg";

import diceRed01 from "./assets/dice-red-1.svg";

function Dice(props) {
  console.log(props)
  const diceImg = props.color === "red" ? diceRed01 : diceBlue01;
  return <img src={diceImg} alt="파란 주사위01" />;
}

export default Dice;

```

- `{color: 'red'}` 객체가 출력된다.
- 빨간 주사위가 나타난다.

#### 2) App.js

```react
import Dice from './Dice.js'

function App(){
  return (
    <div>
      <Dice 
        color="red"/>
    </div>
  )
}

export default App;
```

- `Props`로 red색상을 넣어준다. 

<br/>

## 9.2. 컴포넌트 내부에서 사용방법

### 9.2.1. `Props` 활용 (2)

#### 1) Dice.js

```react
import diceBlue01 from './assets/dice-blue-1.svg'
import diceBlue02 from './assets/dice-blue-2.svg'
import diceBlue03 from './assets/dice-blue-3.svg'
import diceBlue04 from './assets/dice-blue-4.svg'
import diceBlue05 from './assets/dice-blue-5.svg'
import diceBlue06 from './assets/dice-blue-6.svg'

import diceRed01 from './assets/dice-red-1.svg'
import diceRed02 from './assets/dice-red-2.svg'
import diceRed03 from './assets/dice-red-3.svg'
import diceRed04 from './assets/dice-red-4.svg'
import diceRed05 from './assets/dice-red-5.svg'
import diceRed06 from './assets/dice-red-6.svg'

const DICE_IMAGE = {
  blue:[diceBlue01, diceBlue02, diceBlue03, diceBlue04, diceBlue05, diceBlue06],
  red:[diceRed01, diceRed02, diceRed03, diceRed04, diceRed05, diceRed06]
}

function Dice(props){
  const src = DICE_IMAGES[props.color][props.num-1]
  const alt =`${props.color} ${props.num}` 
  return <img src={src} alt={alt}/>
}

export default Dice;
```

- 객체와 배열을 통해 이미지들을 정렬한다.
- 여기서`props`라는 값을 반복하여 사용하고 있기 때문에, 객체구조분해로 `props`를 받아오면 더욱 깔끔한 코드가 될 수 있다.

```react
const DICE_IMAGE = {
  blue:[diceBlue01, diceBlue02, diceBlue03, diceBlue04, diceBlue05, diceBlue06],
  red:[diceRed01, diceRed02, diceRed03, diceRed04, diceRed05, diceRed06]
}

function Dice({color, num}){
  const src = DICE_IMAGES[color][num-1]
  const alt =`${color} ${num}` 
  return <img src={src} alt={alt}/>
}
```

- 또한 객체 구조분해를 할 떄, props 실수로 생략할 수 도 있으니, 기본값을 지정해줄 수 있다. 

```react
function Dice({ color = "blue", num = 1 }) {
  const src = DICE_IMAGES[color][num - 1];
  const alt = `${color} ${num}`;
  return <img src={src} alt={alt} />;
}
```

- `color` Prop의 기본 값은 `blue`로 지정하고, `num` Prop의 기본값은 1로 지정한다.

<br/>

#### 2) App.js

```react
import Dice from './Dice.js'

function App(){
  return (
    <div>
      <Dice 
        color="blue"
        num={1}/>
    </div>
  )
}

export default App;
```

- `num` Prop에서 Prop을 추가할 때, 숫자를 표현하려면, `{}`로 감싸줘야 한다.

<br/>
