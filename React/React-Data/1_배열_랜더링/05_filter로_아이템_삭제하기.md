# 05. filter로 아이템 삭제하기

- `filter` 메서드를 통해서, 데이터 삭제

<br/>

## 05.1. filter & find 

- 배열의 메서드에서 원하는 조건에 맞는 요소들만 추려내서, 새로운 배열로 반환한다.

- 주의할 점은, return문으로 값을 반환하는 것이 아니라, `true` 혹은 `false`라는 조건식에 맞게 리턴을 한다.
  - 즉, 콜백함수가 리턴하는 조건식이 `true`가 되는 요소들만 모아서, 새로운 배열로 `return`을 한다.
- filter 메서드는 항상 return 값이 배열이다. 
- 따라서, 하나의 요소만 출력하기 위해서는 `spread` 요소로 배열을 벗겨 내야 한다.
  - `...`
- 또는 유일한 하나의 값만 찾고자 한다면, `find` 메서드를 활용한다.
- 두 메서드의 차이점은 반복하는 횟수에서 차이가 있다.
  - `find` 의 경우, 조건에 만족하는 하나의 값만 찾기 때문에, 배열을 전체 다 보는 것이 아닌, 찾는 순간 반복을 종료료한다.
  - `filter`의 경우, 조건에 만족하는 값을 모두 찾기 때문에, 배열 전체를 다 실행한다.

<br/>

## 05.2. filter 메서드 적용

### 05.2.1. filter 메서드를 통해서 삭제기능을 추가

#### 1) App.js

```react
import ReviewList from "./ReviewList";
// 2. mockItems로 변경
import mockItems from "../mock.json";
import {useState} from 'react'

function App(){
    // 2-1.
    const [items, setItems] = useState(mockItems)
    const [order, setOrder] = useState('createdAt') // 1. order
    const sortedItems = items.sort((a,b)=> b[order] - a[order]) // 2.
    // 최신순
    const handleNewestClick = () => setOrder('createdAt')
    // 별점순 
    const handleBestClick = () => setOrder('rating')

    // 1. 삭제기능
    const handleDelete = (id) => {
        const nextItems.filter((item)=>{
            item.id != id
        })
        setItems(nextItems) // 3.
    }
    return (
    	<div>
            <div>
            	<button onClick={handleNewestClick} >최신순</button>
                <button onClick={handleBestClick} >베스트순</button>
            </div>
            // 4.
        	<ReviewList items={sortedItems} onDelete={handleDelete}/>
        </div>
    )
}
```

1. `id` 를 파라미터로 받아와서, 해당 `id` 값을 가진 요소를 `filter` 로 걸러준다.
   - 걸러진 item들을 `nextItems`라는 새로운 변수로 적용
   - 새로운 배열 값을 react로 재랜더링한다.

2. `mockItems`라는 이름으로 mock.json을 받고,
   1. item으로 새롭게 State를 받는다.
3. 새로운 배열의 값을, `setItems`로 지정한다.
4. `<ReviewList />` 컴포넌트에 prop으로 내려준다. 

<br/>

#### 2) ReviewList.js - ReviewList

```react
function ReviewList({ items, onDelete }) {
  return (
    <ul>
      {items.map((item) => {
        return (
          <li key={item.id}>
            <ReviewListItem item={item} onDelete={onDelete} />
          </li>
        );
      })}
    </ul>
  );
}

export default ReviewList;
```

- `onDelete` prop을 추가한다.

<br/>

#### 3) ReviewList.js - ReviewListItem

```react
function ReviewListItem({ item, onDelete }) {
   // 1.
  const handleDeleteClick = () => onDelete(item.id);

  return (
    <div className="ReviewListItem">
      <img className="ReviewListItem-img" src={item.imgUrl} alt={item.title} />
      <div>
        <h1>{item.title}</h1>
        <p>{item.rating}</p>
        <p>{formatData(item.createdAt)}</p>
        <p>{item.content}</p>
        <button onClick={handleDeleteClick}>삭제하기</button>
      </div>
    </div>
  );
}
```

- `onDelete` prop을 받고, `handleDeleteClick` 함수를 만들어준다.
- `onDelete` 함수로, item.id 값을 넘겨준다.

<br/>

### 05.2.2. Logic 정리하기

- 사용자가 `삭제하기` 버튼을 누르면, `handleDeleteClick`이 실행이 되고, `onDelete`함수를 실행하는데, 파라미터로, `item.id` 값을 받아준다.
- 이때, `onDelete`함수를 보면, `<ReviewListItem />` 컴포넌트에 `onDelete={handleDelete}` prop이고, 
- 이 prop은 다시, `App.js` 컴포넌트에서,    `<ReviewList items={sortedItems} onDelete={handleDelete} />`  처럼, `handleDelete` 함수로 prop을 받고 있다.

##### _handleDelte 함수_

```js
const handleDelete = (id) => {
    const nextItems.filter((item)=>{
        item.id != id
    })
    setItems(nextItems) // 3.
}
```

- `handleDelte`함수에 파라미터로 해당요소의 id가 전달이 되고, 그 `id` 값을 바탕으로 걸러낸 새로운 배열을 `setItems`로 전달한다.