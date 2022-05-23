# 6. JSX에서 자바스크립트 사용하기

- JSX문법 안에서 `{ }` 를 활용하면 자바스크립트와 관련된 표현식들을 활용할 수 있다.

<br/>

## 6.1. JSX와 JS

- JSX코드는 실제로 실행이 될 떄, JS코드로 변환이 되어 실행이 된다. 
- 따라서, JS코드도 함께 작성이 될 수 있다.

### 6.1.1. JSX에서 HTML과 JS를 함께 사용하는 방법

```react
import ReactDOM from 'react-dom';

const product = '맥북'

ReactDOM.render(
  <h1>나만의 {product} 주문하기</h1>,
  document.getElementById('root'));
```

- `{}` 중괄호로 감싸주고, 변수 이름을 작성한다.  그렇게하면, js코드를 활용할 수 있다. 

<br/>

```react
import ReactDOM from 'react-dom';

const product = 'MacBook'
const model = 'Air'
const item = product + model

const imageUrl = 'https://upload.wikimedia.org/wikipedia/commons/thumb/1/1e/MacBook_with_Retina_Display.png/500px-MacBook_with_Retina_Display.png';

function handleClick(){
  alert('곧 도착합니다.')
}

ReactDOM.render(
  <>
  <h1>나만의 {item.toUpperCase()} 주문하기</h1>
  <img src={imageUrl} alt="제품 사진"/>
  <button onClick={handleClick}>확인</button>
  </>,
  document.getElementById('root'));

```

- 이벤트 헨들러를 사용할 때, `addEventListener` 보다는 요소의 속성값으로 넣어준다.
- 이때, 이벤트는 `카멜케이스(camelCase)`로 사용한다.
- 주의할점은, `{}` 안에는 자바스크립트 표현식만 사용할 수 있다. 따라서, if문 for문, 함수선언과 같은 자바스크립트 문장은 사용할 수 없다. 

<br/>



![6_1](https://github.com/ohtaekwon/TIL/blob/master/React-Basic/img/6_1.png?raw=true)

![6_2](https://github.com/ohtaekwon/TIL/blob/master/React-Basic/img/6_2.png?raw=true)

