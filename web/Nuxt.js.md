

# 👩‍💻Nuxt.js

* Google Trends - Nuxt.js
* 2018년도부터 부상한 Vue 프레임워크
* Vue 프레임워크 기반 개발환경 구축에 도움을 주는 프레임워크
* 서버사이드 렌더링(SSR), 자동 경로 생성, 메타 태그 관리, SEO 개선 등의 기능 제공
* 서버 및 클라이언트 코드 배포의 세부사항을 추상화해 Application 개발에 집중할 수 있게 도와줌

<br>

## 특징
* SPA를 신속하게 만들 수 있다.
* Nuxt.js 설치만으로 이미 scaffolding(프로젝트 구조화)을 해주므로 딱히 프로젝트 구조에 대해서 고민할 필요가 없다.
* Vue.js 하나하나 잡아줘야 할 라우팅을 Nuxt.js에서 파일을 생성하는 것만으로 라우팅을 자동으로 생성해 준다.
* layout, store, middleware와 같은 요소들을 이미 구분을 지어주고 필요한 항목들을 처리해주기 때문에 순전히 개발에만 집중하면 된다.
* Server-Side-Rendering에 필요한 요소가 이미 준비가 되어있다.
* webpack을 통한 빌드 시스템이 이미 구현되어 있다. 그저 npm run만 해주면 된다.
* Nuxt.js 는 nuxt generate 라는 배포 옵션을 제공한다. nuxt generate를 통해 vue.js를 정적인 응용 프로그램으로 빌드한다.

<br>

## 디렉토리 구조 차이
![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/698f23c8-4868-4bba-901e-3af327b0690d)

* 전반적으로 Vue.js 프로젝트의 src 폴더 아래에 있던 코드들이 루트 레벨로 올라옴
* Vue.js 프로젝트의 router 와 view 폴더를 Nuxt.js에선 pages 폴더가 대신함
* Vue.js 프로젝트에서 router/index.js에서 직접 라우터를 등록해주던 것과 달리 Nuxt.js는 pages 폴더 구조대로 라우터를 생성해줌


<hr>

### 참고자료
- [Nuxt.js 란? 개념과 예제](https://doozi0316.tistory.com/m/entry/Nuxtjs-의-개념과-예제-SSR-CSR-Universal)
- [nuxt.js란](https://doozi316.github.io/vue/2021/03/23/Vue9/)
