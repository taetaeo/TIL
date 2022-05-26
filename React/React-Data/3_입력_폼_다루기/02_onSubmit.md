# 02. onSubmit

- `전송` 을 하는 기능을 추가한다.

<br/>

## 02.1. 리액트에서 전송 폼 만들기

- 입력 폼에 입력된 내용들은 `onSubmit` 을 통해서 전송한다.

<br/>

### 02.1.1. type 속성 "submit"

- type 속성이 submit인 경우 그 버튼을 눌렀을 때, `from` 태그안에서 onSubmit이 발생한다.

#### 1) ReviewForm.js 

```react
function ReviewFomr(){
   
  const handleSubmit = ()=>{
      preventDefault()
      console.log({
          title,
          rating,
          content
      })
  }
  return (
    <form className="ReviewForm" onSubmit={handleSubmit}>
      <input value={title} onChange={handleTitleChange} />
      <input type="number" value={rating} onChange={handleRatingChange} />
      <textarea value={content} onChange={handleContentChange} />
      <button type="submit">확인</button> {/* submit 버튼 추가*/}
    </form>
  );
}
```

1. `submit` type인 버튼을 추가한다. 

   - `submit`으로 지정을하면, 버튼을 클릭했을 때, `<form />` 태그에서 `onSubmit` 이벤트가 발생한다.

2. `const handleSubmit` 함수를 만들고, 일단은 콘솔 출력만 한다. 
3. 다음으로, `<form/>` 태그에 `onSubmit={handleSubmit}` 로, 이벤트 함수를 지정한다. 

<br/>

#### [주의] 동작이 새로고침이 발생한다.

- 왜냐하면, HTML `form` 태그의 기본 동작은 `submit`을 눌렀을 때, 입력 폼의 값과 함께 get Request를 보내주게 된다. 
- 따라서, 기본 동작을 막아줘야 한다. 
- `preventDefault()` 함수를 사용한다. 

<br/>

## 02.2. 코드

### 02.2.1. ReviewForm.js

```react
import { useState } from "react";

function ReviewForm() {
  // State
  const [title, setTitle] = useState("");
  const [rating, setRating] = useState(0);
  const [content, setContent] = useState("");

  // Event Handler
  const handleTitleChange = (e) => {
    setTitle(e.target.value);
  };
  const handleRatingChange = (e) => {
    const nextRating = Number(e.target.value) || 0;
    setRating(nextRating);
  };
  const handleContentChange = (e) => {
    setContent(e.target.value);
  };

  // submit
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log({
      title,
      rating,
      content,
    });
  };
  return (
    <form className="ReviewForm" onSubmit={handleSubmit}>
      <input value={title} onChange={handleTitleChange}></input>
      <input type="number" value={rating} onChange={handleRatingChange}></input>
      <textarea value={content} onChange={handleContentChange} />
      <button type="submit">확인</button>
    </form>
  );
}

export default ReviewForm;

```

