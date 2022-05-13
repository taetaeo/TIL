# 7. JSX 정리

## 7.1. JSX란?

- JSX는 자바스크립트의 확장 문법인데요. 리액트로 코드를 작성할 때 HTML 문법과 비슷한 이 JSX 문법을 활용하면 훨씬 더 편리하게 화면에 나타낼 코드를 작성할 수가 있게 됩니다.

<br/>

## 7.2. JSX 문법

- JSX는 자바스크립트로 HTML과 같은 문법을 사용할 수 있도록 만들어주는 편리한 문법이지만, 그만큼 꼭 지켜야 할 규칙들도 있습니다.

<br/>

### 7.2.1. HTML과 다른 속성명

#### 1) 속성명은 카멜 케이스로 작성하기

JSX 문법에서도 태그에 속성을 지정해 줄 수 있습니다. 단, 여러 단어가 조합된 몇몇 속성들을 사용할 때는 반드시 카멜 케이스(Camel Case)로 작성해야 합니다. 사실 여러 단어가 조합된 HTML 속성들이 많진 않지만, 예를 들면 `onclick`, `onblur`, `onfocus` 등과 같은 이벤트 속성이나, `tabindex` 같은 속성들이 있습니다. 이런 속성들은 모두 `onClick`, `onBlur`, `onFocus`, `onMouseDown`, `onMouseOver`, `tabIndex` 처럼 작성하는 것이죠!

```react
import ReactDOM from 'react-dom';

ReactDOM.render(
  <button onClick= ... >클릭!</button>,
  document.getElementById('root')
);
```

단, 예외적으로 HTML에서 비표준 속성을 다룰 때 활용하는 `data-*` 속성은 카멜 케이스(Camel Case)가 아니라 기존의 HTML 문법 그대로 작성하셔야 합니다.

```react
import ReactDOM from 'react-dom';

ReactDOM.render(
  <div>
    상태 변경: 
    <button className="btn" data-status="대기중">대기중</button>
    <button className="btn" data-status="진행중">진행중</button>
    <button className="btn" data-status="완료">완료</button>
  </div>,
  document.getElementById('root')
);
```

<br/>

#### 2) 자바스크립트 예약어와 같은 속성명은 사용할 수 없다.

[React 공식문서 - 어트리뷰트의 차이](https://ko.reactjs.org/docs/dom-elements.html#differences-in-attributes)

- JSX 문법도 결국은 자바스크립트 문법이기 때문에, `for`나 `class`처럼 자바스크립트의 문법에 해당하는 예약어와 똑같은 이름의 속성명은 사용할 수 없습니다. 
- 그래서 HTML의 `for`의 경우에는 자바스크립트의 반복문 키워드 `for`와 겹치기 때문에 `htmlFor`로, HTML의 `class` 속성도 자바스크립트의 클래스 키워드 `class`와 겹치기 때문에 `className`으로 작성해 주어야 합니다.

```react
import ReactDOM from 'react-dom';

ReactDOM.render(
  <form>
    <label htmlFor="name">이름</label>
    <input id="name" className="name-input" type="text" />
  </form>,
  document.getElementById('root')
);
```

<br/>

#### 3) 반드시 하나의 요소로 감싸기 - Frament

- JSX 문법을 활용할 때는 반드시 하나의 요소로 감싸주어야 한다. 그래서 아래 코드처럼 여러 개의 요소를 작성하면 오류가 발생한다. 

```react
import ReactDOM from 'react-dom'

ReactDOM.render(
	<p>안녕</p>
    <p>리액트!</p>,
    document.getElementById('root')
)
```

- 이럴 때는 아래 코드처럼 여러 태그를 감싸는 부모 태그를 만들어 하나의 요소로 만들어 주어야 합니다.

```react
import ReactDOM from 'react-dom';

ReactDOM.render(
  <div>
    <p>안녕</p>
    <p>리액트!</p>
  </div>,
  document.getElementById('root')
);
```

- 하지만 이렇게 작성한다면 때로는 꼭 필요하지 않은 부모 태그가 작성될 수 있겠죠? 그럴 땐 `Fragment`로 감싸주면 의미 없는 부모 태그를 만들지 않아도 여러 요소를 작성할 수 있습니다.

```react
import { Fragment } from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <Fragment>
    <p>안녕</p>
    <p>리액트!</p>
  </Fragment>,
  document.getElementById('root')
);
```

- 참고로 `Fragment`는 아래 코드처럼 빈 태그로 감싸는 단축 문법으로 활용할 수도 있습니다.

```react
import ReactDOM from 'react-dom';

ReactDOM.render(
  <>
    <p>안녕</p>
    <p>리액트!</p>
  </>,
  document.getElementById('root')
);
```

<br/>

#### 4) 자바스크립트 표현식 넣기

- JSX문법에서 중괄호 (`{}`)를 활용하면 자바스크립트 표현식을 넣을 수 있다.

```react
import ReactDOM from 'react-dom';

const product = '맥북';

ReactDOM.render(
  <h1>나만의 {product} 주문하기</h1>,
  document.getElementById('root')
);
```

- 이런 부분들을 잘 활용하면, 아래 코드처럼 중괄호 안에서 문자열을 조합할 수도 있고 변수에 이미지 주소를 할당해서 `img` 태그의 `src` 속성값을 전달해 줄 수도 있고, 이벤트 핸들러를 좀 더 편리하게 등록할 수도 있습니다.

```react
import ReactDOM from 'react-dom';

const product = 'MacBook';
const model = 'Air';
const imageUrl = 'https://upload.wikimedia.org/wikipedia/commons/thumb/1/1e/MacBook_with_Retina_Display.png/500px-MacBook_with_Retina_Display.png'

function handleClick(e) {
  alert('곧 도착합니다!');
}

ReactDOM.render(
  <>
    <h1>{product + ' ' + model} 주문하기</h1>
    <img src={imageUrl} alt="제품 사진" />
    <button onClick={handleClick}>확인</button>
  </>,
  document.getElementById('root')
);
```

- 단, JSX 문법에서 중괄호는 자바스크립트 **표현식**을 다룰 때 활용하기 때문에, 
- 중괄호 안에서 for, if문 등의 문장은 다룰 수 없다는 점은 꼭 기억해 주세요. 
- 그런데도 만약 JSX 문법을 활용할 때 조건문이 꼭 필요하다면 조건 연산자를, 반복문이 꼭 필요하다면 배열의 반복 메소드를 활용해 볼 수는 있겠죠?