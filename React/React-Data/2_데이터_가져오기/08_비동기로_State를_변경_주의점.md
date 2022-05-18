# 08. 비동기로 State를 변경할 때, 주의할 점

- 더보기 기능의 버그

<br/>

## 08.1. 더보기 기능의 버그

- `Show 3G` 의 상태에서 `더 보기` 버튼을 누르고 곧 바로, `삭제` 버튼을 눌렀을 경우,
- 삭제된 데이터가 데이터 로딩이 완료되면 다시 나타나게 된다. 

<br/>

### 08.1.1. 버그 수정

- 왜 이런 버그가 발생하는가?
- `더 보기` 버튼을 누르면 `handleLoadMore`가 실행이 되고, 
- 그 함수는, `handleLoad({ order, offset, limit: Limit });`  즉, order, offset, limit 값으로, `handleLoad`를 실행한다. 
- 이 시점에서 `items` State 값은 삭제 버튼을 누르기전 State 값이다. 
- 그리고, `handleLoad` 함수에서도 `setItems([...items, ...reviews])` 삭제버튼을 누르기전 `items` State 값이다.
- 여기서, `getReveiew`라는 비동기 함수를 호출하는데, 네트워크를 보내는 동안 다른 작업이 실행되는데, 즉,  `삭제` 버튼 눌렀을 때이다.
- `handleDelete` 함수가 호출이 되고, 거기서 `items` State를 변경해서 요소를 하나 없앤다. 
- 그렇게 되면, 요소가 지워진 채로 랜더링이 되고, 
- 그러던 중에 다시 비동기 함수인 , `getReveiew`의 response가 도착을 해서, `State`를 변경하려고 하는데, 이떄 `items` State 값은 함수 내에서는 삭제되기 전의 `items` State 값이다. 
- 그곳에서 새로 받아온 데이터를 추가하면, 지웠던 데이터가 다시 살아난 것처럼 보이게 된다. 
- 이렇게 비동기로 State를 변경할 때는, 잘못된 시점의 값을 사용하는 문제가 있다.
- 이럴때는, 콜백을 전달해서 해결할 수 있다. 

#### 1) App.js

```react
function App(){
	//.... 생략
    
  const handleLoad = async (options) => {
    const { reviews, paging } = await getRewviews(options);
    if (options.offset === 0) {
      setItems(reviews);
    } else {
      setItems((prevItems)=>[...prevItems, ...reviews]);
    }
    setOffset(options.offset + reviews.length); // 6
    setHasNext(paging.hasNext);
  };
}
```

- `setItems((prevItems)=>[...prevItems, ...reviews]);`
- `prevItems` 라는 파라미터로 이전 State값을 받아서, 변경할 State값을 리턴하면 된다. 
- 이때, `prevItems`값은 고정된 것이 아니라, 함수의 파라미터이기 때문에, React가 현재시점의 State를 전달하게 된다. 