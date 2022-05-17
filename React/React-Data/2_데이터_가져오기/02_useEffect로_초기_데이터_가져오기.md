# 02. useEffect로 초기 데이터 가져오기

## 02.1. 페이지를 열었을 때, 데이터 자동 출력

### 02.1.1. `useEffect` 

#### 1) App.js

```react
// 프로젝트의 최상위 컴포넌트
import ReviewList from "./ReviewList";
import { useEffect, useState } from "react";
import { getRewviews } from "../api";

function App() {
  const [items, setItems] = useState([]);
  const [order, setOrder] = useState("createdAt");
  const sortedItems = items.sort((a, b) => b[order] - a[order]);
  // 최신순
  const handleNewstClick = () => {
    setOrder("createdAt");
  };
  // 평점순
  const handleBestClick = () => {
    setOrder("rating");
  };
  // 삭제
  const handleDelete = (id) => {
    console.log("handleDelete", items);
    const nextItems = items.filter((item) => item.id !== id);
    setItems(nextItems);
  };

  const handleLoad = async () => {
    const { reviews } = await getRewviews();
    setItems(reviews);
  };
  // 1. useEffect
  useEffect(() => {
    handleLoad();
  }, []);

  return (
    <div>
      <div>
        <button onClick={handleNewstClick}>최신순</button>
        <button onClick={handleBestClick}>평점순</button>
      </div>
      <ReviewList items={sortedItems} onDelete={handleDelete} />
      {/* <button onClick={handleLoadClick}>불러오기</button> */}
    </div>
  );
}
export default App;
```

1. `useEffect()`함수에 실행할 콜백 함수와 빈 배열을 넘겨주게 되면, React는 콜백함수를 맨 처음 랜더링할때만 실행하기 때문에, 무한루프가 생기는 것을 막을 수 있다. 

<br/>

## 02.2. 정리하자면,

- 컴포넌트가 처음 랜더링이 될 때, 리퀘스트를 보내고 싶다면, `useEffect`를 사용해야 한다.