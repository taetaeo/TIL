# 02. useEffect로 초기 데이터 가져오기

- `불러오기` 버튼을 클릭해서 데이터를 불러오는 것이 아니라, 페이지를 열었을 때, 자동으로 불러오도록 한다.

<br/>

## 02.1. 페이지를 열었을 때, 데이터 자동 출력

### 02.1.1. 무한 루프 발생

#### 1) App.js

- 먼저, 앞서 만든 `불러오기` 버튼 태그는 지운다.
- 그다음, `handleLoadClick` 함수는 `handleLoad` 로 바꿔준다.

```react
function App() {
 // ...생략
  const handleLoad = async () => {
    const { reviews } = await getRewviews();
    setItems(reviews);
  };
  // 1. handleLoad함수 실행
  handleLoad()

  return (
    <div>
      <div>
        <button onClick={handleNewstClick}>최신순</button>
        <button onClick={handleBestClick}>평점순</button>
      </div>
      <ReviewList items={sortedItems} onDelete={handleDelete} />
    </div>
  );
}
export default App;
```

1. `handleLoad()` 함수를 실행시켜주면, 무한루프가 발생해서 request를 계속 보낸다.

<br/>

#### [참고] 무한 루프가 발생하는 이유?

- 처음 **App** 컴포넌트를 랜더링할 때 리액트는 `App()` 함수를 실행하는데, 한 줄씩 코드를 실행하다가 `handleLoad()` 함수를 실행한다. 
- 다음 코드로 넘어와서, JSX구문인 리액트 엘리먼트들을 리턴하면서 화면을 그려준다.
- `handleLoad` 함수를 살펴보면 비동기로 request를 보냈다가 response가 도착하면, `reviews` 로 변수를 지정하고, `setItems`를 통해서 State를 변경해준다.
- 그렇게 되면, 리액트는 `App()` 함수를 다시 실행하고, 이때 다시 `handleLoad()` 함수를 실행해서  State를 변경해주는 로직을 실행하고 다시 랜더링되면서 무한 루프가 발생하게 된다.
- 이러한 경우를 대비하기 위해  리액트에서는 `useEffect()` 함수를 사용한다.,

<br/>

### 02.1.2. `useEffect` 

- 컴포넌트가 처음 랜더링이 될 때, 리퀘스트를 보내고 싶다면, `useEffect`를 사용해야 한다.

```react
import ReviewList from "./ReviewList";
import { useEffect, useState } from "react";
import { getReviews } from "../api";

function App() {
  // State
  // Item State
  const [items, setItems] = useState([]);
  // order State
  const [order, setOrder] = useState("createdAt");
  // 정렬 - 내림차순
  const sortedItems = items.sort((a, b) => b[order] - a[order]);

  // 이벤트 핸들러
  // 버튼 - 정렬
  const handleNewestClick = () => setOrder("createdAt");
  const handleBestClick = () => setOrder("rating");
  // 버튼 - 삭제
  const handleDelete = (id) => {
    const nextItems = items.filter((item) => item.id !== id);
    setItems(nextItems);
  };
  // 데이터 불러오기
  const handleLoad = async () => {
    const { reviews } = await getReviews();
    setItems(reviews);
  };
  // 1. useEffect 함수 실행
  useEffect(() => {
    handleLoad();
  }, []);

  return (
    <div>
      <div>
        <button onClick={handleNewestClick}>최신순</button>
        <button onClick={handleBestClick}>평점순</button>
      </div>
      <ReviewList items={sortedItems} onDelete={handleDelete} />
    </div>
  );
}

export default App;
```

1. `useEffect()`함수에 실행할 콜백 함수와 빈 배열을 넘겨주게 되면, React는 콜백함수를 맨 처음 랜더링할때만 실행하기 때문에, 무한루프가 생기는 것을 막을 수 있다. 
