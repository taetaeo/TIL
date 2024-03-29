# 09. useState 정리

- `useState` 의 초깃값을 지정하는 다른 방법들

<br/>

## 09.1. 초깃값 지정하기

```js
const [state, setState] = useState(initialState);
```

- `useState` 함수에 값을 전달하면 초깃값으로 지정할 수 있다.

<br/>

### 09.1.1. 콜백으로 초깃값 지정하기

```js
const [state, setState] = useState(() => {
  // 초기값을 계산
  return initialState;
});
```

- 초깃값을 계산해서 넣는 경우 이렇게 콜백을 사용하면 좋다.

<br/>

#### `getSavedValues` 라는 함수를 통해서 컴퓨터에 저장된 초깃값을 가져올 때,

```js
function ReviewForm() {
  const savedValues = getSavedValues(); // ReviewForm을 렌더링할 때마다 실행됨
  const [values, setValues] = useState(savedValues);
  // ...
}
```

- 이 코드에서의 문제점은 `savedValues` 라는 값은 처음 렌더링 한 번만 계산하면 되는데, 
- 매 렌더링 때마다 불필요하게 `getSavedValues` 함수를 실행해서 저장된 값을 가져온다.

```js
function ReviewForm() {
  const [values, setValues] = useState(() => {
    const savedValues = getSavedValues(); // 처음 렌더링할 때만 실행됨
    return savedValues
  });
  // ...
}
```

- 이렇게 콜백형태로 초깃값을 지정해주면, 처음 랜더링 할 때 한 번만 콜백을 실행해서 초깃값을 만들고, 그 이후로 콜백을 실행하지 않기 때문에, `getSavedValues`를 불필요하게 실행하지 않는다. 
- 이 때, 주의할 점은 이 콜백 함수가 리턴할 때까지 리액트가 랜더링하지 않고 기다린다.
  - 따라서, 콜백 함수의 실행이 오래 걸릴수록 초기 랜더링이 늦어질 수 있다.


<br/>

## 09.2. Setter 함수 사용하기

### 09.2.1. 기본

```js
const [state, setState] = useState(0);

const handleAddClick = () => {
  setState(state + 1);
}
```

- Setter 함수에다가 값을 전달하면, 해당하는 값으로 변경된다.
- 이때 주의할 점이 있는데, 배열이나 객체 같은 참조형은 반드시 새로운 값을 만들어서 전달해야 한다.
- 따라서, `...` 를 사용해야 한다.

<br/>

### 09.2.2. 참조형 State 사용 잘못된 예

```js
const [state, setState] = useState({ count: 0 });

const handleAddClick = () => {
  state.count += 1; // 참조형 변수의 프로퍼티를 수정
  setState(state); // 참조형이기 때문에 변수의 값(레퍼런스)는 변하지 않음
}
```

<br/>

### 09.2.3. 참조형 State 사용의 올바른 예

```js
const [state, setState] = useState({ count: 0 });

const handleAddClick = () => {
  setState({ ...state, count: state.count + 1 }); // 새로운 객체 생성
}
```

<br/>

### 09.2.4. 콜백으로 State 변경

```js
setState((prevState) => {
  // 다음 State 값을 계산
  return nextState;
});
```

- 만약 이전 State 값을 참조하면서 State를 변경하는 경우, 
- 비동기 함수에서 State를 변경하게 되면 최신 값이 아닌 State 값을 참조하는 문제가 있었다.
- 이럴 때는 **콜백**을 사용해서 처리할 수 있다.
-  파라미터로 올바른 State 값을 가져와서 사용할 수 있습니다. 
- **이전 State 값으로 새로운 State를 만드는 경우엔 항상 콜백 형태를 사용하는 습관을 들이면 좋다.**

<br/>

### 09.2.5. 콜백으로 State를 변경하는 예시

```js
const [count, setCount] = useState(0);

const handleAddClick = async () => {
  await addCount();
  setCount((prevCount) => prevCount + 1);
}
```

