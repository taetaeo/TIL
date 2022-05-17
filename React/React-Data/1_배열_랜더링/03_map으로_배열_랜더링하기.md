# 03. map으로 배열 랜더링하기

- `map` 배열 메서드를 통해서, 각 데이터를 랜더링한다.

<br/>

## 03.1. map 메서드

- `map()` 메서드는 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환합니다.

```js
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]

```

<br/>

### 03.1.1. map 메서드 적용

#### 1) ReviewList.js

```react
function ReviewList( { items }){
    return <ul> {items.map((item)=>{
            // 1. JSX return
            return <li> {item.title} </li>
        })}</ul>
}
export default ReviewList
```

1. `map` 메서드안에서, `JSX` 리턴을 하면, `JSX`를 여러개 추가한 것 처럼 동작을 한다.

![03_1](https://github.com/ohtaekwon/TIL/blob/master/React/React-Data/1_%EB%B0%B0%EC%97%B4_%EB%9E%9C%EB%8D%94%EB%A7%81/img/03_1.png?raw=true)

- 요소 하나에 해당하는 컴포넌트들을 만든다.

<br/>

#### 2) ReviewList.js

```react
// 4. style
import "../css/ReviewList.css";

// 3. formDate
function formDate(value){
    const date = new Date(value);
 	return `${data.getFullYear()}. ${data.getMonth() + 1}. ${data.getDate()}`;
}

// 2. ReviewListItem
function ReviewListItem( {item} ){
    return (
    	<div className="ReviewListItem">
        	<img className="ReviewListItem-img" src={item.imgUrl} alt={item.title} />
        	<div>
            	<h1>{item.title} </h1>
                <p> {item.rating} </p>
                <p> {formDate(item.createdAt)} </p>
                <p> {item.content} </p>
            </div>
        </div>
    
    )
}


function ReviewList( { items }){
    return <ul> {items.map((item)=>{
            // 4.
            return <li> <ReviewListItem item={item} /></li>
        })}</ul>
}
export default ReviewList
```

2. `<ReviewListItem />` 컴포넌트를 만든다.
3. `formDate`를 만든다.
4. `<ReviewListItem />`  
   - `<li>` 태그마다. `<ReviewListItem />`  컴포넌트를 return하고,
   - `item` prop를 전달한다.
   - `item` prop은 callback함수의 파라미터인 `item`으로 받는다. 

![](https://github.com/ohtaekwon/TIL/blob/master/React/React-Data/1_%EB%B0%B0%EC%97%B4_%EB%9E%9C%EB%8D%94%EB%A7%81/img/03_2.png?raw=true)