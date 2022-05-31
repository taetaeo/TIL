# 09. ref와 useRef 정리

- DOM 노드를 참조할 때, `useRef` 함수로, Ref 객체를 만들고, 이것의 `current` 라는 프로퍼티를 활용한다.

<br/>

## 09.1. Ref 객체 생성

```react
import {useRef} from 'react';

const ref = useRef();
```

- `useRef` 함수로 Ref 객체를 만들 수 있다.

<br/>

## 09.2. `ref ` Prop 사용하기

 ```react
 const ref = useRef();
 
 // ...
 
 <div ref={ref}>...</div>
 ```

- `ref` Prop에다가 앞에서 만든 Ref 객체를 내려주면 된다.

<br/>

## 09.3. Ref 객체에서 DOM 노드 참조하기

```react
const node = ref.current;

if (node) {
    // node를 사용하는 코드
}
```

- Ref 객체의 `current` 라는 프로퍼티를 사용하면, `DOM` 노드를 참조할 수 있다.
- `currnet` 값은 없을 수도 있으니까 반드시 값이 존재하는지 검사하고 사용해야 한다.

<br/>

## 09.4. 이미지 크기 구하기

- 다음의 코드는 `img` 노드의 크기를 `ref` 를 활용해서 출력하는 예시이다.
- `img` 노드에는 너비 값인 `width` 와 높이 값인 `height`라는 속성이 있다.
- Ref 객체의 `current` 로 DOM 노드를 참조해서 두 속성 값을 가져온다.

```react
import { useRef } from 'react';

function Image({ src }) {
  const imgRef = useRef();
  const handleSizeClick = () => {
    const imgNode = imgRef.current;
    if (!imgNode) return;

    const { width, height } = imgNode;
    console.log(`${width} x ${height}`);
  };
  return (
    <div>
      <img src={src} ref={imgRef} alt="크기를 구할 이미지" />
      <button onClick={handleSizeClick}>크기 구하기</button>
    </div>
  );
}
```

