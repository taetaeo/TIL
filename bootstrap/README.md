# Bootstraps

[더 알아보기](https://getbootstrap.com/docs/5.1/getting-started/introduction/)

## CSS

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
```

## Bundle

```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
```

## POPJS

[poperJS 더 알아보기](https://popper.js.org/) 

- 터미널에서 다음과 같이 입력

```sh
npm i @popperjs/core 
```

<br/>

## NPM 프로젝트 생성

- 터미널에서, 다음의 코드를 입력

```sh
npm init -y
npm i -D parcel-bundler
```

- `package.json` 파일로 들어간 후, `script` 에서
  - `"dev":"parcel index.html"`
  - `"build ": "parcel build index.html"`

- 다시 터미널에서 부트스트랩을 설치한다.

```sh
npm install bootstrap
```

- js에서 적용하기 위해서 
  - `import bootsatrp from 'bootstrap/dist/js/bootstrap.bundle'`

- css에서 적용하기 위해서는
  - `@import "../node_modules/bootstrap/scss/bootstrap.scss"`

## Cutomize

 [더 알아보기](https://getbootstrap.com/docs/5.1/customize/overview/)

```scss
// Required
@import "../node_modules/bootstrap/scss/functions";
@import "../node_modules/bootstrap/scss/variables";
@import "../node_modules/bootstrap/scss/mixins";

$theme-colors: (
  "primary":    $primary,
  "secondary":  yellowgreen,
  "success":    $success,
  "info":       $info,
  "warning":    $warning,
  "danger":     $danger,
  "light":      $light,
  "dark":       $dark
);

@import "../node_modules/bootstrap/scss/bootstrap.scss";

```

