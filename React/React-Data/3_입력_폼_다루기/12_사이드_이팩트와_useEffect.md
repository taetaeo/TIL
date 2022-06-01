# 12. 사이드 이팩트와 useEffect



## 12.1. 사이드 이팩트(Side Effect)란?

- 사이드 이팩트는 한국어로 '부작용'이라는 의미이다.
- 일상생활에서는 '약의 부작용'처럼 사용하는 단어인데, 예를 들면 감기약을 먹었을 때,
  - 감기 증상은 없어졌지만 (작용) 
  - **피부가 붉게 올라오면 (부작용)**
- 이 약에는 부작용이 있다고 할 수 있다. 일상생활에서는 주로 안 좋은 것들을 부작용이라고 부르지만,
- 프로그래밍에선 말 그대로 외부에 부수적인 작용을 하는 걸 말한다.

```react
let count = 0;

function add(a, b) {
  const result = a + b;
  count += 1; // 함수 외부의 값을 변경
  return result;
}

const val1 = add(1, 2);
const val2 = add(-4, 5);
```

- 위 코드에서 `add` 함수를 보면, 이 함수는 `a`, `b` 를 파라미터로 받아서 더한 값을 리턴한ㄷ.
- 함수 코드 중에서 함수 바깥에 있는 `count` 라는 변수의 값을 변경하는 코드가 있는데, `add` 함수는 실행하면서 함수 외부의 상태(count 변수)가 바뀌기 때문에, 이런 함수를 **"사이드 이펙트가 있다"**고 합니다.
- 우리에게 친숙한 예로는 `console.log` 함수가 있는데, 이렇게 함수 안에서 함수 바깥에 있는 값이나 상태를 변경하는 걸 '사이드 이펙트'라고 부른다.

<br/>

## 12.2. 사이드 이펙트와 useEffect

- `useEffect` 는 리액트 컴포넌트 함수 안에서 **사이드 이펙트를 실행하고 싶을 때** 사용하는 함수이다.
- 예를들면 DOM 노드를 직접 변경한다거나, 브라우저에 데이터를 저장하고, 네트워크 리퀘스트를 보내는 것들이 있다.
- 주로 **리액트 외부에 있는 데이터나 상태를 변경할 때** 사용한다.
- 간단한 예시들을 보면서 어떤 식으로 활용할 수 있는지 가볍게 살펴봅시다.

<br/>

### 12.2.1. 페이지 정보 변경

```react
useEffect(() => {
  document.title = title; // 페이지 데이터를 변경
}, [title]);
```

<br/>

### 12.2.2. 네트워크 요청

```react
useEffect(() => {
  fetch('https://example.com/data') // 외부로 네트워크 리퀘스트
    .then((response) => response.json())
    .then((body) => setData(body));
}, [])
```

<br/>

### 12.2.3. 데이터 저장

```react
useEffect(() => {
  localStorage.setItem('theme', theme); // 로컬 스토리지에 테마 정보를 저장
}, [theme]);
```

- 참고: `localStorage` 는 웹 브라우저에서 데이터를 저장할 수 있는 기능입니다.

<br/>

### 12.2.4. 타이머

```react
useEffect(() => {
  const timerId = setInterval(() => {
    setSecond((prevSecond) => prevSecond + 1);
  }, 1000); // 1초마다 콜백 함수를 실행하는 타이머 시작
  
  return () => {
    clearInterval(timerId);
  }
}, []);
```

- 참고: `setInterval` 이라는 함수를 쓰면 일정한 시간마다 콜백 함수를 실행할 수 있습니다.

<br/>

## 12.3. useEffect를 쓰면 좋은 경우

