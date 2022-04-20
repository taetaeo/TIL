# SCSS (Sass)

[sass-lang.com 더 알아보기](https://sass-lang.com/)

- css 전처리 도구
- sass의 문법에서 css와 호환을 하기 위해서 제공한 것이 바로, scss이다.

- sass의 경우 `;` 와 `{}` 가 없다. 따라서, 시각적으로 보기 편리한 것이 scss이다.

## 왜 SCSS를 사용할까?

- 중첩기능이 있기 때문에, CSS만 작성했을 때의 불편함을 줄일 수 있다.

## SCSS에서 CSS 변환

- SCSS문법은 브라우져에서 작동하지 않기 때문에, CSS로 변환을 해야한다.
- 이때 변환을 하는 과정을 `컴파일(complile)`이라고 한다.
- 즉, scss코딩을 한 후, css로 변환해서 사용해야 한다.

## scss 사용방법

- 터미널에서 `npm` 설치

```sh
npm init -y
npm i -D parcel-bundler
```

- `package.json` 파일에 들어가서, `script` 부분에 다음과 같이 작성
  -   `"dev": "parcel index.html",`
  -   `"build": "parcel build index.html"`

- `index.html` 파일에서  scss 파일 연결

```html
 <link rel="stylesheet" href="./main.scss"/>
```

<br/>

# SCSS이용해보기

## 1. codepen.io

[codepen.io 들어가기](https://codepen.io/following)

- 해당 사이트에서 scss를 적용해볼 수 있다.
- View compiled CSS를 누르면 변환이된 CSS 결과물을 볼 수 있다.

## 2. sassmeister

[sassmeister](https://www.sassmeister.com/)

- 해당 사이트에서 scss에서 전처리된 css문법을 보여준다.
