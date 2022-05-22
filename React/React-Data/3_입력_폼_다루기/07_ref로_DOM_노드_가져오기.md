# 07. ref로 DOM 노드 가져오기

- 

<br/>

## 07.1. DOM 노드에 접근하기 - ref

- `ref` 라는 prop은 원하는 시점에 실제 DOM 노드에 접근하고 싶을 때, 사용할 수 있는 prop이다.

<br/>

### 07.1.1. ref객체 만들기

#### 1) FileInput.js

```react
import { useEffect, useRef } from "react";

function FileInput({ name, value, onChange }) {
  // 1. ref객체 만들기
  const inputRef = useRef();
  const handleChange = (e) => {
    const nextValue = e.target.files[0];
    onChange(name, nextValue);
  };
  // 2. useEffect
  useEffect(() => {
    console.log(inputRef);
  }, []);

  return <input type="file" onChange={handleChange} ref={inputRef} />;
}

export default FileInput;
```

1. `useRef()` 라는 함수로 ref객체를 만들고, `input`의 `ref`라는 prop으로 내려준다. 

2. `useEffect` 라는 함수를 사용해서, 처음 랜더링이 되었을 때만, `inputRef`를 콘솔로 보여준다. 
3. `<input /> ` 태그에 `ref` prop을 내려준다.

![7_1](https://github.com/ohtaekwon/TIL/blob/master/React/React-Data/3_%EC%9E%85%EB%A0%A5_%ED%8F%BC_%EB%8B%A4%EB%A3%A8%EA%B8%B0/img/7_1.png?raw=true)

![7_2](https://github.com/ohtaekwon/TIL/blob/master/React/React-Data/3_%EC%9E%85%EB%A0%A5_%ED%8F%BC_%EB%8B%A4%EB%A3%A8%EA%B8%B0/img/7_2.png?raw=true)

- 콘솔에 출력된, `ref` 객체에는 `current` 프로퍼티가 있고, input에 마우스를 가져다대면, 화면에 랜더링이 되느,  `Fileinput`을 가리킨다.

- 이런식으로, `ref`를 쓰면, 실제 DOM 노드를 직접 참조할 수 있다. 

#### [주의할 점] DOM노드는 반드시 랜더링이 끝나야 생기니까, ref객체의 current 값도 화면에 컴포넌트가 랜더링이 됐을 떄만, 존재한다.

- 조건부 랜더링으로 컴포넌트가 사라지는 경우에는 이 값이 없을 수도 있으므로, 아래와 같이 조건식을 한다.

```react
function FileInput({name, value, onChange}){
   // .......생략.........
   useEffect(() => {
    if (inputRef.current){
      console.log(inputRef.current);
    }
  }, []);

}
```

- 항상 `inputRef.currnet` 이 존재하는지 확인하고, 사용하는 것을 권장한다.

![7_3](https://github.com/ohtaekwon/TIL/blob/master/React/React-Data/3_%EC%9E%85%EB%A0%A5_%ED%8F%BC_%EB%8B%A4%EB%A3%A8%EA%B8%B0/img/7_3.png?raw=true)