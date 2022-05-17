# 02. mock 데이터 추가하기

- JSON 데이터를 랜더링한다.

<br/>

## 02.1. 프로젝트 세팅

### 02.1.1. 파일 정리

- `public` 폴더에 `index.html` 파일과 `src` 폴더의 `index.js` 파일을 제외한 나머지 파일을 삭제하고 정리한다.

#### 1) index.js - React 18 버전 이전

```react
import ReactDOM from 'react-dom'

ReactDOM.render(<h1>안녕 리액트</h1>, document.getElementById('root'))
```

<br/>

#### 2) index.js - React 18 버전 이후

```react
import ReactDom from "react-dom/client";

const root = ReactDom.createRoot(document.getElementById("root"));
root.render(<App />);
```

<br/>

### 02.1.2. mock.json 파일 불러오기

- `mock` 데이터란, 네트워크로 불러올 데이터를 흉내내기 위한 데이터

- `src` 폴더에 `mock.json` 파일을 불러온다.

<br/>

### 02.1.3. `components` 폴더 생성

- `src` 폴더에 `components` 폴더를 생성 후, 
- `<component/>` 들을 구성한다.

<br/>

#### 1) ReviewList.js

```react
function ReviewList( { items }){
    console.log(items)
    return <ul></ul>
}

export default ReviewList
```

- `<ReviewList />` 컴포넌트에서 `items` 배열을 props를 받는다.

<br/>

#### 2) App.js

- 프로젝트의 최상위 컴포넌트

```react
// ReviewList 컴포넌트를 불러온다.
import ReviewList from './ReviewList';

// mock데이터를 불러온다.
import items from '../mock.json'

function App(){
    return (
        <div> 
          <ReviewList items={items} / > 
        </div>
       )
}
export default App;
```

- `items` 이름으로 `mock.json` 파일을 import하고, 
- `<ReviewList />`  컴포넌트에 `items` prop으로 내려준다.

<br/>

#### 3) index.js

- `<App />` 컴포넌트를 랜더링한다.

```react
import ReactDom from "react-dom/client";
import App from "./components/App";

const root = ReactDom.createRoot(document.getElementById("root"));
root.render(<App />);
```

<br/>

## 02.2. mock.json 

```
[
    {
        "id": 38,
        "title": "소리꾼 디오리지널",
        "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/3eb7b297-19c7-4e9b-870e-b7796c981d68.jpg",
        "rating": 2,
        "content": "영조 10년, 사라진 아내 간난을 찾아 나선 소리꾼 학규와 그의 딸 청이. 학규를 중심으로 뭉친 새로운 광대패들과 함께 흥과 한이 담긴 조선팔도의 여정이 시작된다. 가족을 찾기 위한 학규의 울림있는 외침 \"우리는 다시 만나야 한다!\"",
        "createdAt": 1625065200000,
        "updatedAt": 1625065200000
    },
    {
        "id": 32,
        "title": "기도하는 남자",
        "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/2c12da43-306a-4708-adff-081594785d68.jpg",
        "rating": 3,
        "content": "지독한 경제난 속에서 개척교회를 운영 중인 목사 ‘태욱’(박혁권)은 설상가상으로 아내 ‘정인’(류현경)으로부터 장모(남기애)의 수술비가 급히 필요하다는 이야기를 전해 듣는다.  극한의 상황 속에서 태욱과 정인은 각기 다른 선택의 기로에 놓이고, 믿음에 어긋나는 상상 속에서 그들은 처절하게 갈등하는데…  우리를 시험에 들게 하지 마시옵고, 다만 악에서 구하시옵소서",
        "createdAt": 1616511600000,
        "updatedAt": 1616511600000
    },
    {
        "id": 36,
        "title": "뮬란",
        "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/003fb945-15b4-4515-9536-c606d99aef43.jpg",
        "rating": 2,
        "content": "무예에 남다른 재능을 지닌 ‘뮬란’은 좋은 집안과 인연을 맺어 가문을 빛내길 바라는 부모님의 뜻에 따라 본연의 모습을 억누르고 성장한다. 어느 날, 북쪽 오랑캐들이 침입하자 황제는 징집령을 내리고 ‘뮬란’은 아픈 아버지를 대신해 가족들 몰래 전장에 나가기로 결심한다.  여자라는 게 발각되면 목숨을 잃을 수도 있는 상황 속에서 ‘뮬란’은 타고난 용기와 지혜로 역경을 이겨내며 전사로 성장한다.  마침내 잔인무도한 적장 ‘보리 칸’과 마녀 ‘시아니앙’을 마주하게 된 ‘뮬란’. 그녀는 위험에 빠진 동료와 가족을 구하고 진정한 전사로 거듭날 수 있을 것인가",
        "createdAt": 1600268400000,
        "updatedAt": 1600268400000
    },
    {
        "id": 30,
        "title": "테넷",
        "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/a3833ea5-5e60-4e9c-afb3-957cb30cb768.jpg",
        "rating": 3,
        "content": "시간의 흐름을 뒤집는 인버전을 통해 현재와 미래를 오가며 세상을 파괴하려는 사토르(케네스 브래너)를 막기 위해 투입된 작전의 주도자(존 데이비드 워싱턴). 인버전에 대한 정보를 가진 닐(로버트 패틴슨)과 미술품 감정사이자 사토르에 대한 복수심이 가득한 그의 아내 캣(엘리자베스 데비키)과 협력해 미래의 공격에 맞서 제3차 세계대전을 막아야 한다!",
        "createdAt": 1598367600000,
        "updatedAt": 1598367600000
    },
..........생략........
    {
        "id": 35,
        "title": "내가 살인범이다",
        "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/21edba04-42cd-4bad-8d77-d5add53ad84d.jpg",
        "rating": 3,
        "content": "15년 전, 세상을 떠들썩하게 만들었던 연곡 연쇄살인 사건. 하지만 이 사건은 끝내 범인을 잡지 못한 채 공소시효가 끝난다. 사건 담당 형사 최형구는 범인을 잡지 못한 죄책감과 자신의 얼굴에 끔찍한 상처를 남기고 사라진 범인에 대한 분노로 15년 간 하루도 편히 잠들지 못한다. 그리고 2년 후, 자신을 연쇄 살인사건의 범인이라고 밝힌 이두석이 ‘내가 살인범이다’라는 자서전을 출간하고, 이 책은 단숨에 베스트셀러가 된다. 미남형 외모와 수려한 말솜씨로 스타가 된 이두석. 최형구는 알려지지 않은 마지막 미해결 실종사건을 파헤쳐 세상이 용서한 이두석을 어떻게든 잡아넣으려 하는데…  법이 용서한 연쇄살인범  공소시효는 끝났지만, 사건은 아직 끝나지 않았다!",
        "createdAt": 1352300400000,
        "updatedAt": 1352300400000
    },
    {
        "id": 41,
        "title": "화차",
        "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/c57e10d0-561d-4906-889a-4779f8ef8543.jpg",
        "rating": 3,
        "content": "결혼 한 달 전, 부모님 댁에 내려가던 중 휴게소에 들른 문호와 선영. 커피를 사러 갔다 온 문호를 기다리고 있는 건 문이 열린 채 공회전 중인 차 뿐이다. 꺼져있는 휴대폰, 흔적도 없이 그녀가 사라졌다. 그녀를 찾기 위해 전직 강력계 형사인 사촌 형 종근에게 도움을 청한 문호. 하지만 가족도 친구도 없는 그녀의 모든 것은 가짜다. 실종 당일, 은행잔고를 모두 인출하고 살던 집의 지문까지 지워버린 선영의 범상치 않은 행적에 단순 실종사건이 아님을 직감하는 종근은 그녀가 살인사건과 연관되어 있음을 알아낸다. 그녀는 과연 누구였을까? 그녀의 정체에 다가갈수록 점점 더 충격적인 진실들이 밝혀지기 시작 하는데…",
        "createdAt": 1331132400000,
        "updatedAt": 1331132400000
    },
    {
        "id": 28,
        "title": "홀리데이",
        "imgUrl": "https://learn-codeit-kr-static.s3.ap-northeast-2.amazonaws.com/react-02/film-reviews/84160fe5-7857-4e56-925d-aafc98b9d181.jpg",
        "rating": 2,
        "content": "1988년 10월... 올림픽이라는 세계적인 행사를 끝마치고 세계 4위라는 감흥에서 빠져 나오지 못했던 그 때... 징역 7년, 보호감호 10년형을 받아 복역중인 지강혁과 죄수들이 호송차를 전복 탈출하는 세상을 깜짝 놀라게 하는 사건이 발생한다. 권총 1정과 실탄을 빼앗아 무장탈주에 성공한 강혁과 일당들은 원정강도와 가정집을 돌며 인질극을 벌이는 등 서울을 공포의 도가니로 몰아넣는다. 하지만 인질로 잡힌 사람들은 매스컴에서 말하는 흉악범이라는 이야기와 달리 인간적이고 예의바른 강혁 일당에게 연민의 정을 느끼게 된다.  그렇게 탈주 9일째 되던 날, 북가좌동의 가정집에 숨어있던 강혁 일당은 자신들을 끈질기게 쫓던 경찰관 안석에게 발각되고 경찰과 최후의 대치극을 펼치게 된다. 강혁의 마지막 소원인 비지스의 'Holiday'가 울려 퍼지는 가운데 지강혁은 자신들을 둘러 싸고 있는 경찰과 매스컴을 향해 외친다. \"유전무죄, 무전유죄. 돈이 있으면 죄가 없고 돈이 없으면 죄가 된다...\"  강혁의 외침은 TV 등 매스컴을 통해 전국으로 울려 퍼지고, 강혁은 일당들과 함께 최후의 선택을 하게 되는데...",
        "createdAt": 1137596400000,
        "updatedAt": 1137596400000
    }
]
```

