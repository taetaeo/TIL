# 5. Fragment

- `JSX` 문법으로 HTML 태그를 작성할 때는, 반드시 하나로 감싸진 태그로 작성을 해야한다.

<br/>

## 5.1. JSX에서 Fragment

- 하나로 감싸진 태그가 아닌, 두 개 이상의 태그로 만든다면, 오류가 발생한다.

<br/>

### 5.1.1. Fragement 사용하는 이유

- JSX에서 문법 오류가 발생할 때,

```react
import ReactDOM from 'react-dom'

ReactDOM.render(
	<P>안녕</P>
    <P>리액트</P>,
    document.getElementById('root')
)
```

- 이렇게 작성을 하면, 오류 메시지가 나온다. 
- "JSX 요소들은 반드시 하나의 요소로 감싸줘야 한다."는 오류가 발생한다.

```react
import ReactDOM from 'react-dom'

ReactDOM.render(
    <div>
	<P>안녕</P>
    <P>리액트</P>
    </div>,
    document.getElementById('root')
)
```

- 이와같이 `<div>` 태그로 감싸주면서, 하나로 감싸주면서 오류가 발생하지 않았다.
- 만약 `<div>` 태그를 쓰고 싶지 않을 때는?
  - `JSX` 에서 제공하는 `Fragment`를 사용한다.

<br/>

### 5.1.2. Fragment 사용방법

```react
import { Fragment } from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <Fragment>
      <h1 id="title">안녕 리액트!</h1>
      <button className="hand">가 위</button>
      <button className="hand">바 위</button>
      <button className="hand">보</button>
  </Fragment>,
  document.getElementById('root'));

```

- `<Fragment/>`로 길게 사용하기 보다는 이름이 없는 태그형태인 축약형으로 사용할 수 있다.
  - `<> </>`

```react
import { Fragment } from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <>
      <h1 id="title">안녕 리액트!</h1>
      <button className="hand">가 위</button>
      <button className="hand">바 위</button>
      <button className="hand">보</button>
  </>,
  document.getElementById('root'));
```

<br/>

![5_1](https://github.com/ohtaekwon/TIL/blob/master/React-Basic/img/5_1.png?raw=true)