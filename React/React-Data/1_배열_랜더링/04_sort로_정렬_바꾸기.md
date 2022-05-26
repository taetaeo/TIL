# 04. sort로 정렬 바꾸기

- `sort` 배열 메서드를 통해서, 각 데이터를 정렬한다.

<br/>

## 04.1. sort & reverse

### 04.1.1 sort 메서드

- 배열에서 `sort`라는 메소드를 활용하면 배열을 정렬할 수 있습니다.
-  `sort` 메소드에 아무런 아규먼트도 전달하지 않을 때는 기본적으로 [유니코드](https://ko.wikipedia.org/wiki/유니코드)에 정의된 문자열 순서에 따라 정렬됩니다.

```js
const letters = ['D', 'C', 'E', 'B', 'A'];
const numbers = [1, 10, 4, 21, 36000];

letters.sort();
numbers.sort();

console.log(letters); // (5) ["A", "B", "C", "D", "E"]
console.log(numbers); // (5) [1, 10, 21, 36000, 4]
```

- 그렇기 때문에 `numbers`에 `sort` 메소드를 사용한 것 처럼, 숫자를 정렬할 때는 우리가 상식적으로 이해하는 오름차순이나 내림차순 정렬이 되지 않습니다.

- 그럴 땐 `sort` 메소드에 다음과 같은 콜백함수를 아규먼트로 작성해주면 된다.

```js
const numbers = [1, 10, 4, 21, 36000];

// 오름차순 정렬
numbers.sort((a, b) => a - b);
console.log(numbers); // (5) [1, 4, 10, 21, 36000]

// 내림차순 정렬
numbers.sort((a, b) => b - a);
console.log(numbers); // (5) [36000, 21, 10, 4, 1]
```

- `sort` 메소드를 사용할 때 한 가지 주의해야될 부분은 **메소드를 실행하는 원본 배열의 요소들을 정렬**한다는 점입니다. 
- 그래서 한 번 정렬하고 나면 정렬하기 전의 순서로 다시 되돌릴 수 없으니, 그런 경우에는 미리 다른 변수에 복사해두는 것이 권장된다.

<br/>

### 04.1.2. 오름차순, 내림차순 정렬시 a-b와 b-a가 의미하는것

- 반환 값 < 0 : a가 b보다 앞에 있어야 한다.

- 반환 값 = 0 : a와 b의 순서를 바꾸지 않는다.

- 반환 값 > 0 : b가 a보다 앞에 있어야 한다.

<br/>

### 04.1.3. reverse 메서드

- `reverse` 메소드는 말 그대로 배열의 순서를 뒤집어 주는 메소드 입니다. 
- `reverse` 메소드는 별도의 파라미터가 존재하지 않기 때문에 단순이 메소드를 호출해주기만 하면 배열의 순서가 뒤집히는데요. 
- `sort` 메소드와 마찬가지로 **원본 배열의 요소들을 뒤집어 버린다**는 점은 꼭 주의헤야 합니다.

```js
const letters = ['a', 'c', 'b'];
const numbers = [421, 721, 353];

letters.reverse();
numbers.reverse();

console.log(letters); // (3) ["b", "c", "a"]
console.log(numbers); // (3) [353, 721, 421]
```

<br/>

## 04.2. sort 메서드 적용

### 04.2.1.  `sort()` 정렬 메서드

#### 1) App.js

```react
import ReviewList from "./ReviewList";
import items from "../mock.json";

function App(){
    // 1. rating 내림차순 정렬
    const sortedItems = items.sort((a,b)=> b.rating - a.rating)
    return (
    	<div>
        	<ReviewList items={sortedItems} />
        </div>
    )
}
```

1. 내림차순 정렬하는 변수를 만들고, prop로, 전달한다.
   - 작은 순서대로 정렬(오름차순): `items.sort((a, b) => a - b)`
   - 크기가 큰 순서대로 정렬(내림차순): `items.sort((a, b) => b - a)`

<br/>

- 정렬기준을 정렬기준으로 prop를 변경하여 전달하도록 하려면? 
  - `state`를 활용한다.

```react
import ReviewList from "./ReviewList";
import items from "../mock.json";
import { useState } from "react";

function App() {
  // order State 
  const [order, setOrder] = useState('createdAt')

  // 정렬 - 내림차순
  const sortedItems = items.sort((a, b) => b[order] - a[order]); 

  return (
    <div>
      <ReviewList items={sortedItems} />
    </div>
  );
}

export default App;

```

<br/>

### 04.2.2. 사용자가 State값을 선택하도록 지정

- 정렬기준을 최신순과 별점순을 선택하도록 한다.
- prop를 변경하여 전달하도록 하려면? 
  - `state`를 활용한다.

#### 1) App.js

```react
import ReviewList from "./ReviewList";
import items from "../mock.json";

function App(){
    // 1. order State 
    const [order, setOrder] = useState('createdAt') 
    // 2. 정렬 - 내림차순
    const sortedItems = items.sort((a,b)=> b[order] - a[order]) 
    // 3. 이벤트 핸들러
    // 3-1. 최신순
    const handleNewestClick = () => setOrder('createdAt')
    // 3-2.별점순 
    const handleBestClick = () => setOrder('rating')

    return (
    	<div>
            <div>
            	<button onClick={handleNewestClick} >최신순</button>
                <button onClick={handleBestClick} >베스트순</button>
            </div>
        	<ReviewList items={sortedItems} />
        </div>
    )
}
```

1. order state를 만들고, 기본값을 `createdAt`로 한다.
2. `order` 의 기준에 따라, 최신순, 별점순을 적용하도록 한다.
3. 이벤트 핸들러 함수를 만들어서 버튼 클릭시에, 정렬 기준을 변경하도록 한다.
   1. 최신순을 선택하도록 하는 setOrder에 기본값 `createdAt` 을 적용한다.
   2. 별점순을 선택하도록 하는 setOrder에 기본값 `rating` 을 적용한다.
4. 버튼을 만들고 Prop으로 핸들러 함수를 내려준다. 