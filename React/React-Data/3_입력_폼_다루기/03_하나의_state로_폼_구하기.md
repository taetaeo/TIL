# 03. 하나의 state로 폼 구하기

- 입력 폼에서 여러개로 관리하던 State를 하나의 State로 통합적으로 관리한다.
- `input` 태그의 `name` 속성을 활용하는 것이 핵심이다.

<br/>

## 03.1. 하나의 State로 관리하기

### 03.1.1. `<input>` 태그의 `name` 속성을 활용

- 이벤트 객체에서 `name` 값을 가져올 수 있다.

#### 1) ReviewForm.js - State(1)

```react
function ReviewForm() {
  // Input State
  // Title State
  const [title, setTitle] = useState("");
  // rating State
  const [rating, setRating] = useState(0);
  // content State
  const [content, setContent] = useState("");
}
```

- 우선 `title`, `rating` , `content` 각각의 State를 지우고, 하나의 객체 State를 만든다.

<br/>

#### 2) ReviewForm.js - State(2)

```react
function App(){
    const [values, setValues] = useStaet({
        title:'',
        rating:0,
        content:''
    });
}
```

- `value` State를 만들고, 초기값으로는 각 `input`의 필드값을 넣어준다. 

< br/>

#### 3) ReviewForm.js - 이벤트 핸들러

```react
function App(){
  const handleTitleChange = (e) => {
    setTitle(e.target.value);
    console.log("handleTitle : ", e.target.value);
  };

  const handleRatingChange = (e) => {
    const nextRating = Number(e.target.value) || 0;
    setRating(nextRating);
  };

  const handleContentChange = (e) => {
    setContent(e.target.value);
  };

}
```

- 기존의 각각의 이벤트 핸들러를 지우고 통합적 객체 관리를 위한 새로운 핸들러 함수를 만든다. 

<br/>

#### 4) ReviewForm.js

```react
function App(){
    //... 생략....
    
    const handleChange = () =>{
        // 1. 이벤트 객체의 target에서 
        const {name,value} = e.target
        // 2. setter
        setValue((prevValues)=>{
            ...prevValues,
            [name] : value
        })
        
    }
}
``
```

1. 이벤트 객체의 `target` 에서 `name` 값과 `value` 값을 가져온다. 
2. `[name]` 프로퍼티에 value를 지정해준다.
   - `[]` 로 지정하면, `name` 의 값으로 프로퍼티를 지정하고, 해당하는 값(value)를 지정해줄 수 있다. 

<br/>

#### 5) ReviewForm.js - handleSubmit

```react
function App(){
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(values);
  };
}
```

- 출력 :

```
{
    "title": "닥터스트레인지",
    "rating": "4",
    "content": "그럭저럭 볼만함\n"
}`
```

<br/>

#### 6) ReviewForm.js - JSX

```react
  return (
    <form className="ReviewForm" onSubmit={handleSubmit}>
      <input name="title" value={values.title} onChange={handleChange} />
      <input
        name="rating"
        type="number"
        value={values.rating}
        onChange={handleChange}
      />
      <textarea name="content" value={values.content} onChange={handleChange} />
      <button type="submit">확인</button>
    </form>
  );
```

- 이제 onCange에 prop을 `handleChange`로 바꿔준다.
- 그다음, State의 값도 바꿔준다.`values.State값`

- 그 후, `name` 의 값을 지정해준다.

<br/>

## 03.2.  모던한 프로퍼티 표기법

### 03.2.1. 객체 프로퍼티 작성

#### 1) 기존의 객체 작성법

```js
const user = {
    title : 'tk',
    birth : 2022,
    jobs : '프론트엔드'
}
```

#### 2) 변수에 할당해서 프로퍼티 값 적용

```js
const title = 'tk'
const birth = '2022'
const job = '프론트엔드'

const user = {
    title : title,
    birth = birth,
    job : job,
};
```

- 활용할 name 과 프로퍼티의 name이 같다면, 생략이 가능하다

```js
const user = {
    title,
    birth,
    job,
};
```

<br/>

#### 3) 프로퍼티 name과 함수의 name이 같을 때, 

```js
function getFullName(){
    return `${this.firstName} ${this.lastName}`
}

const user = {
	firstName : 'tk',
    lastNaem : 'oh',
    getFullName
}

const admin = {
    firstName : 'Alex',
    lastName : 'kim',
    getFullName
}

console.log(user.getFullName) // tk oh
console.log(admin.getFullName) // Alex kim
```

<br/>

#### 4) 프로퍼티 name을 표현식으로 나타내는 방법

```js
// 계산된 속성명 (computed property name)
const user ={
    [표현식] : 값
}
```

- 표현식을 `[]` 로 감싸주게 되면, 표현식의 값을 프로퍼티 name으로 쓸 수 있게 된다.

```js
const user = {
    ['oh' + 'tk'] = 'value'
}

console.log(user) // {ohtk : 'value'}