# 02. onSubmit

## 02.1. 리액트에서 전송 폼 만들기

### 01.1.1. onSubmit

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

#### [주의] 동작이 새로고침이 된다. 

- 왜냐하면, HTML `form` 태그의 기본 동작은 `submit`을 눌렀을 때, get Request를 보내주게 된다. 
- 따라서, 기본 동작을 막아줘야 한다. 
- `preventDefault()` 함수를 사용한다. 