# Vue.js 설치방법

## 1. 프로토타입 설치

프로토 타이핑의 목적으로 CDN을 통해 이용할 수 있다.

```html
<script src="https://unpkg.com/vue@next"></script>
```

<br/>

## 2. CLI

Vue.js는 단일 페이지 애플리케이션를 빠르게 구축할 수 있는 [공식 CLI (opens new window)](https://github.com/vuejs/vue-cli)를 제공합니다. 최신 프론트엔드 워크 플로우를 위해 사전 구성된 빌드 설정을 제공합니다. 핫 리로드, 저장시 린트 체크 및 프로덕션 준비가 된 빌드로 시작하고 실행하는데 몇 분 밖에 걸리지 않습니다. 상세한 내용은 [Vue CLI 문서 (opens new window)](https://cli.vuejs.org/)에서 찾아보실 수 있습니다.

- 터미널에서 다음과 같이 작성한다.

```bash
npm install -g @vue/cli
```

- [Vue CLI](https://cli.vuejs.org/guide/creating-a-project.html) 에서 create 명령어를 찾는다.

- 터미널에서 다음과 같이 작성한다.
  - `vue create [프로젝트 이름]`
  - `vue 3`를 선택한다.
- 설치가 완료가 되면 다음과 같은 명령어가 나온다
  - `cd [프로젝트 이름]` : 해당 프로젝트로 이동
    - `code .` 를 입력하면 해당 프로젝트로 vsCode로 이동
  - `npm run serve`  :  개발 서버를 여는 명령어 (= `npm run dev` 와 같다.)