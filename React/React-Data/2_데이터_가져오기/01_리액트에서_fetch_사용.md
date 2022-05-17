# 01. 리액트에서 fetch 사용하기

## 01.1. fetch & async / await & Promise

### 01.1.1. `fetch` 함수

- 웹브라우저와 서버가 통신할 때, 요청을 보내는데 웹 브라우저에서 자바스크립트를 사용할 때, `fetch` 함수를 사용한다.

```js
fetch('https://www.google.com')
	.then((res)=>res.text())
	.then((result) => {console.log(result)})
```

- 웹 브라우저는 서버로부터 받은 응답을 해석해서 보여주는 것이다. 

<br/>

### 01.1.2. async / await

- `Promise` 객체를 간단하게 만들고자 할 때, 사용한다.

```js
fetch('https://jsonplaceholder.typicode.com/users')
	.then((res)=>res.text())
	.then((result) => {console.log(result)})
```

- 이 코드를 `async/await` 로 사용하기

```js
async function fetchAndPrint(){
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    const result = await response.text();
    console.log(result);
}

fetchAndPrint();
```

- `async` 는 `asynchronous`의 줄임말로, 비동기를 의미한다. `async`는 함수안에 비동기적으로 실행하는 것이 있다는 것을 의미한다. 
- `await`이 붙어있는 코드가 비동기적으로 실행이 된다. `await`은 뒤에 코드를 실행하고, 그 코드가 `return`하는 `Promise` 객체를 기다려준다. 
- 해당 `Promise` 객체가 `fullfil` 또는 `reject`의 상태가 될 때까지 기다려준다. 
- 그리고나서, `Promise` 객체가 `fullfil` 또는 `reject`의 상태가 되면, 작업의 성공 결과를 추출해서 return 한다.
- 즉, ` await fetch('https://jsonplaceholder.typicode.com/users');` 는, `fetch` 함수가 `return` 하는 `promise` 객체가 `fullfil` 상태가 될 때까지 기다린다. 
- 그리고, `fullfil` 상태가 되면, 작업성공 결과인 `response 객체`를 추출해서 return한다.
- 그리고나면, 다음줄의 코드 `const result = await response.text();` 가 실행이 된다. 
- 여기서도 마찬가지로,  `response` 객체의 `text` 메소드는 `Promise` 객체를 return한다.
- 그 앞의 `await`이 `text()` 메소드가 return한 `promise` 객체가 `fullfil`상태가 될 때까지 기다리고, `fullfil` 상태가 되면, 작업성공 결과를 추출해서 return한다.

<br/>

### 01.1.3. 정리하자면,

- `await`이 그 뒤의 코드를 실행하고, 그것이 return하는 `Promise` 객체가 `fullfiled` 상태가 될 때까지 가디란다. 

- 그리고 해당 `Promise` 객체가 `fullfiled` 상태가 되면, 그 작업 성공 결과를 추출해서 return한다.
- `async` 붙어있는 함수안에 비동기 실행이 있다는 뜻은, 함수의 코드중에서 `Promise` 객체를 return하는 코드가 있다는 의미이다. 

- 그리고 그 앞에는 `await`을 붙여서, `Promise` 객체가 `fullfiled` 상태가 될 때까지 기다리고, 작업 성공 결과를 return한 후에야 다음줄을 실행한다.

<br/>

## 01.2. mock데이터에서 네트워크 데이터

### 01.2.1. fetch 함수로 request

```js
fetch('https://learn.codeit.kr/api/film-reviews')
```

- `Network` 탭에서 결과를 확인하면,

<br/>

```
{
    "reviews": [
        {
            "createdAt": 1625065200000,
            "updatedAt": 1625065200000,
            "id": 38,
            "title": "소리꾼 디오리지널",
            "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/3eb7b297-19c7-4e9b-870e-b7796c981d68.jpg",
            "content": "영조 10년, 사라진 아내 간난을 찾아 나선 소리꾼 학규와 그의 딸 청이. 학규를 중심으로 뭉친 새로운 광대패들과 함께 흥과 한이 담긴 조선팔도의 여정이 시작된다. 가족을 찾기 위한 학규의 울림있는 외침 \"우리는 다시 만나야 한다!\"",
            "rating": 2
        },
        {
            "createdAt": 1616511600000,
            "updatedAt": 1616511600000,
            "id": 32,
            "title": "기도하는 남자",
            "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/2c12da43-306a-4708-adff-081594785d68.jpg",
            "content": "지독한 경제난 속에서 개척교회를 운영 중인 목사 ‘태욱’(박혁권)은 설상가상으로 아내 ‘정인’(류현경)으로부터 장모(남기애)의 수술비가 급히 필요하다는 이야기를 전해 듣는다.  극한의 상황 속에서 태욱과 정인은 각기 다른 선택의 기로에 놓이고, 믿음에 어긋나는 상상 속에서 그들은 처절하게 갈등하는데…  우리를 시험에 들게 하지 마시옵고, 다만 악에서 구하시옵소서",
            "rating": 3
        },
        {
            "createdAt": 1600268400000,
            "updatedAt": 1600268400000,
            "id": 36,
            "title": "뮬란",
            "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/003fb945-15b4-4515-9536-c606d99aef43.jpg",
            "content": "무예에 남다른 재능을 지닌 ‘뮬란’은 좋은 집안과 인연을 맺어 가문을 빛내길 바라는 부모님의 뜻에 따라 본연의 모습을 억누르고 성장한다. 어느 날, 북쪽 오랑캐들이 침입하자 황제는 징집령을 내리고 ‘뮬란’은 아픈 아버지를 대신해 가족들 몰래 전장에 나가기로 결심한다.  여자라는 게 발각되면 목숨을 잃을 수도 있는 상황 속에서 ‘뮬란’은 타고난 용기와 지혜로 역경을 이겨내며 전사로 성장한다.  마침내 잔인무도한 적장 ‘보리 칸’과 마녀 ‘시아니앙’을 마주하게 된 ‘뮬란’. 그녀는 위험에 빠진 동료와 가족을 구하고 진정한 전사로 거듭날 수 있을 것인가",
            "rating": 2
        },
        {
            "createdAt": 1598367600000,
            "updatedAt": 1598367600000,
            "id": 30,
            "title": "테넷",
            "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/a3833ea5-5e60-4e9c-afb3-957cb30cb768.jpg",
            "content": "시간의 흐름을 뒤집는 인버전을 통해 현재와 미래를 오가며 세상을 파괴하려는 사토르(케네스 브래너)를 막기 위해 투입된 작전의 주도자(존 데이비드 워싱턴). 인버전에 대한 정보를 가진 닐(로버트 패틴슨)과 미술품 감정사이자 사토르에 대한 복수심이 가득한 그의 아내 캣(엘리자베스 데비키)과 협력해 미래의 공격에 맞서 제3차 세계대전을 막아야 한다!",
            "rating": 3
        },
        {
            "createdAt": 1596553200000,
            "updatedAt": 1596553200000,
            "id": 22,
            "title": "다만 악에서 구하소서",
            "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/ade0b093-663d-49c6-b930-d90dc399858b.jpg",
            "content": "태국에서 충격적인 납치사건이 발생하고 마지막 청부살인 미션을 끝낸 암살자 인남(황정민)은 그것이 자신과 관계된 것임을 알게 된다. 인남은 곧바로 태국으로 향하고, 조력자 유이(박정민)를 만나 사건을 쫓기 시작한다. 한편, 자신의 형제가 인남에게 암살당한 것을 알게 된 레이(이정재).  무자비한 복수를 계획한 레이는 인남을 추격하기 위해 태국으로 향하는데...  처절한 암살자 VS 무자비한 추격자 멈출 수 없는 두 남자의 지독한 추격이 시작된다!",
            "rating": 3
        },
        {
            "createdAt": 1595948400000,
            "updatedAt": 1595948400000,
            "id": 12,
            "title": "강철비2: 정상회담",
            "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/84dbe34d-a398-494a-a49d-244a09a01712.jpg",
            "content": "북미 평화협정 체결을 위한 대한민국 대통령(정우성), 북한의 최고지도자인 위원장(유연석)과 미국 대통령(앵거스 맥페이든)간의 남북미 정상회담이 북한 원산에서 열린다. 북미 사이 좀처럼 이견이 좁혀지지 않는 가운데, 핵무기 포기와 평화체제 수립에 반발하는 북 호위총국장(곽도원)의 쿠데타가 발생하고, 납치된 세 정상은 북한 핵잠수함에 인질로 갇힌다. 그리고, 좁디 좁은 함장실 안, 예기치 못한 진정한 정상회담이 벌어지게 되는데… 동북아시아의 운명이 핵잠수함에 갇혔다! 과연, 남북미 세 지도자는 전쟁 위기를 막을 수 있을 것인가?",
            "rating": 3
        },
        {
            "createdAt": 1594738800000,
            "updatedAt": 1594738800000,
            "id": 4,
            "title": "반도",
            "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/300c4285-b0e2-42dc-a658-9416bb5bf3e9.jpg",
            "content": "[전대미문의 재난 그 후 4년 폐허의 땅으로 다시 들어간다!] 4년 전, 나라 전체를 휩쓸어버린 전대미문의 재난에서 가까스로 탈출했던 ‘정석’(강동원). 바깥세상으로부터 철저히 고립된 반도에 다시 들어가야 하는 피할 수 없는 제안을 받는다.    제한 시간 내에 지정된 트럭을 확보해 반도를 빠져 나와야 하는 미션을 수행하던 중 인간성을 상실한 631부대와 4년 전보다 더욱 거세진 대규모 좀비 무리가 정석 일행을 습격한다.    절체절명의 순간, 폐허가 된 땅에서 살아남은 ‘민정’(이정현) 가족의 도움으로 위기를 가까스로 모면하고 이들과 함께 반도를 탈출할 수 있는 마지막 기회를 잡기로 한다.    되돌아온 자, 살아남은 자 그리고 미쳐버린 자 필사의 사투가 시작된다!",
            "rating": 3
        },
        {
            "createdAt": 1594134000000,
            "updatedAt": 1594134000000,
            "id": 37,
            "title": "밤쉘: 세상을 바꾼 폭탄선언",
            "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/bc5aaca8-e96f-4a9b-b4f2-f0554ade9048.jpg",
            "content": "대선후보 토론회에서 트럼프와 설전을 벌인 폭스뉴스의 간판 앵커 메긴 켈리(샤를리즈 테론)는 트럼프의 계속되는 트위터 공격으로 화제의 중심에 선다. 한편, 동료 앵커인 그레천 칼슨(니콜 키드먼)은 ‘언론 권력의 제왕’이라 불리는 폭스뉴스 회장을 고소하고 이에 메긴은 물론, 야심 있는 폭스의 뉴페이스 케일라 포스피실(마고 로비) 역시 충격을 감추지 못하는데…   최대 권력을 날려버릴 폭탄선언 이제 이들의 통쾌하고 짜릿한 역전극이 시작된다!",
            "rating": 3
        },
        {
            "createdAt": 1594134000000,
            "updatedAt": 1594134000000,
            "id": 25,
            "title": "그레텔과 헨젤",
            "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/0a47db02-e401-4b6d-9151-9395e83707e3.jpg",
            "content": "옛날 어느 먼 옛날, 그레텔과 헨젤은 먹을 것과 일감을 찾기 위해 집을 떠나지만 길을 잃고 만다. 그들은 허기짐에 먹을 것이 풍성하게 차려진 한 오두막에 이끌려 집으로 들어가게 되고, 그 곳에서 집 주인 ‘홀다’를 만난다. 그녀의 배려로 두 남매는 풍족한 음식과 따뜻한 잠자리를 제공받으며 점점 안정을 되찾는다. 하지만 매일 밤 반복되는 악몽, 매끼 차려지는 성대한 식사, 벽 너머 발견된 의문의 문고리 등   오두막에서 일어나는 기묘하고 섬뜩한 징조들은 두 남매를 계속해서 어둠 속으로 몰아넣는데…",
            "rating": 2
        },
        {
            "createdAt": 1592924400000,
            "updatedAt": 1592924400000,
            "id": 5,
            "title": "#살아있다",
            "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/47ffccf5-c9f3-40b7-9c54-9ad4dabee1c4.jpg",
            "content": "원인불명 증세의 사람들의 공격에 통제 불능에 빠진 도시. 영문도 모른 채 잠에서 깬 ‘준우’(유아인)는 아무도 없는 집에 혼자 고립된 것을 알게 된다. 데이터, 와이파이, 문자, 전화 모든 것이 끊긴 채 고립된 상황. 연락이 두절된 가족에 이어 최소한의 식량마저 바닥이 나자 더 이상 버티기 힘들어진 ‘준우’. 하지만 그 순간 건너편 아파트에서 누군가 시그널을 보내온다. 또 다른 생존자 ‘유빈’(박신혜)이 아직 살아있음을 알게 된 ‘준우’는 함께 살아남기 위한 방법을 찾아 나서는데...! 꼭 살아남아야 한다",
            "rating": 2
        }
    ],
    "paging": {
        "count": 43,
        "hasNext": true
    }
}
```

- `padging` 과 `reviews` 프로퍼티가 response 된다. 

<br/>

### 01.2.2. mock데이터에서 fetch로 받아오기

#### 1) api.js

- `src` 폴더에 `api.js` 파일을 만든다. 
- 여기에 `request` 함수들을 모아서 사용한다. 

```js
export async function getRewviews() {
  const res = await fetch("https://learn.codeit.kr/api/film-reviews");
  console.log(res);
  const body = await res.json(); // json 함수를 호출
  return body;
}
```

- `fetch`를 호출하고 받아온 `response` 바디를 return하는 함수이다. 
- `json()` 함수를 호출하여, JSON변환을 통해서,  JSON 데이터를 javascript 객체로 변환한다.

<br/>

#### [참고] fetch json()메서드

- etch API의 응답(response) 객체는`json()`를 제공하고 있어`JSON.parse()` 대신 사용할 수 있다.

```js
fetch(데이터요청 할 서버 url)
.then(response => response.json())
.then(data => {
  //데이터 처리 부분
}
```

- `response.json()`메서드를 호출하면 JSON 데이터를 javascript 객체로 변환한다.

<br/>

#### [참고] JSON.parse()와 response.json()의 차이

- `JSON.parse()`에는 응답(response) 바디만을 넣어야한다.바디와 헤더가 들어가면 데이터를 읽어오지 못한다
- `response.json()`에는 응답 헤더가 들어가도 바디만 읽어서 불러온다.

<br/>

#### 2) App.js

```react
// 프로젝트의 최상위 컴포넌트
import ReviewList from "./ReviewList";
import { useState } from "react";
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
  // 3.
  const handleLoadClick = async () => {
    const { reviews } = await getRewviews();
    setItems(reviews);
  };

  return (
    <div>
      <div>
        <button onClick={handleNewstClick}>최신순</button>
        <button onClick={handleBestClick}>평점순</button>
      </div>
      <ReviewList items={sortedItems} onDelete={handleDelete} />
      <button onClick={handleLoadClick}>불러오기</button>
    </div>
  );
}

export default App;
```

1. `MockItems`를 제거

2. ` const [items, setItems] = useState([]);` 빈배열을 초기값으로 설정한다.
3. `handleLoadClick` 함수를 만든다. 
   - `import { getRewviews } from "../api";` 를 불러오고,
   - `reviews` 프로퍼티를 `setItems`에 넣는다.
4. `<button onClick={handleLoadClick}>불러오기</button>` 불러오기 버튼을 누르면, 네트워크로 연결된 데이터들이 출력되도록 한다.