# 06. 배열을 랜더링할 때 key

- 배열을 랜더링할 때, key값을 적용한다.

<br/>

## 06.1. key를 써야하는 이유 

- 요소마다 `key` 로 고유값을 지정해주면, 배열의 변화를 react에 정확하게 전달할 수 있다. 

<br/>

### 06.1.1. child 안에 key prop

- `map` 메서드를 통해서 랜더링이 된 것들이 `child` 인데,
- `key` prop을 각각 적용해야 한다.

<br/>

#### 1) ReviewList.js

```react
function ReviewList({ items, onDelete }) {
  console.log(items);
  return (
    <ul>
      {items.map((item) => {
        return (
          <li key={item.id}>
            <ReviewListItem item={item} onDelete={onDelete} />
            <input></input>
          </li>
        );
      })}
    </ul>
  );
}
```

- 배열을 랜더링할 때는 반드시 key를 설정해야 한다.
- 그렇지 않은 경우, 재랜더링이 되었을 때, 위치에 대해 변형된 값이 적용되지 않는다. 
- 각 데이터를 구분할 수 있는 고유한 값으로 `key` 를 설정한다.
  - `id` 값으로 key값을 설정한다.