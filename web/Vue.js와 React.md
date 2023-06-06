# Vue.js 와 React

📣 __프로그레시브 프레임워크__ vs __JavaScript  라이브러리__


> 프레임워크 : 부분적인 사용이 불가능하고,  프레임워크가 지원해주는 문법에 따라 작성해야한다.
> 
> 라이브러리 : 참고가 용이하고, 라이브러리의 일부분만 가져와서 사용하는 것이 편리하다. 

## Vue.js와 React의 차이점

-    **전역 상태 관리, 라우팅, 빌드 시스템 등을 지원 여부**  
👉 `React`는 Redux, Recoil, React-router-dom 등의 별도의 라이브러리를 사용해야만 한다.
- **코드 구성의 차이**  
👉 `React`는 jsx 형태로 코드를 작성한다. 즉, JavaScript를 사용한다.  
  `Vue`는 HTML, CSS, JS 코드 영역을 분리해서 사용한다. 이 때문에  `Vue`가 코드 가독성이 더 좋을 수 있다.
-  **컴포넌트의 차이**  
👉  `React`는 파일별로 컴포넌트를 분리할 수 있으며 props 형태로 전달하거나 재사용하기 용이하다.   
`Vue`는 새로운 컴포넌트를 만들기 위해 새로운 파일을 하나 만들고, template, script, style을 모두 다시 작성해야 한다.

-   **자유도**  
👉 `React`의 진입 장벽이  `Vue`에 비해 더 높다. 라이브러리와 상태 관리, 그리고 관련 미들웨어 등 알아야 할 것이 많기 때문이다.
- **TypeScript 호환도**  
👉 `React`는 TypeScript와의 호환이  `Vue`에 비해 쉽고 자유롭다.
-   **사용량**  
👉 `React`는  `Vue`에 비해 월등히 사용량이 높고 변화에 빠르게 대응한다.



# 👩‍💻 Vue.js
✔️**가상 DOM**  
원본 HTML, DOM을 표현하는 메모리 상의 가벼운 DOM 트리  
원본 DOM에 영향을 미치지 않고 업데이트 가능

✔️**컴포넌트(Component)**  
Vue.js 어플리케이션에서 재사용할 수 있는 엘리먼트로 Vue 인스턴스 생성

✔️**템플릿(Templates)**  
Vue 인스턴스 데이터와 DOM에 접근할 수 있는 HTML  기반의 템플릿 제공

✔️**라우팅(Routing)**  
페이지의 전환은 VUE-ROUTER를 사용

✔️**저용량(Light Weight)**  
다른 프레임워크에 비해 저용량

  
  
  
### Vue.js의 특징
1️⃣ **컴포넌트 기반 프레임워크**
- 유지보수 및 재사용 가능

2️⃣ **MVVM 패턴**
- 뷰(View) : 돔(DOM)
- 뷰 모델(View Model) : Vue.js
- 모델(Model) : 자바스크립트 객체

3️⃣ **Vue Router 사용**

- 페이지 이동 시 서버에 요청해 새로 갱신하는 것이 아니라,  
미리 해당 페이지를 받아놓고 클라이언트의 라우팅을 이용해 화면을 갱신
( Single Page Application 방식 )


# 👩‍💻 React

✔️**가상 DOM**  
원본 HTML, DOM을 표현하는 메모리 상의 가벼운 DOM 트리  
원본 DOM에 영향을 미치지 않고 업데이트 가능

✔️**컴포넌트(Component)**  
요소라고 하는 컴포넌트 별로 나누어 개발이 가능하며, 다른 곳에 활용할 수도 있다.

✔️**JavaScript 기반**  
별도의 프레임워크를 배울 필요가 없으며, JavaScript를 그대로 활용한다.

✔️**선언형**  
UI를 만들 때 쉽고 간결하게 해준다, 애플리케이션 안의 상태에 따른 디자인 뷰와 연결된 데이터가 변경되면 이에 맞는 컴포넌트들을 올바르게 렌더링해 화면 구성을 해준다.


### React의 특징

1️⃣ **컴포넌트 기반의 라이브러리**
- 유지보수 및 재사용 가능

2️⃣ **단방향 데이터 바인딩(One Way Data Flow)**

- React는 데이터의 흐름이 한 방향으로만 흐른다.  
데이터가 내려가기만 하고 밑에서 데이터를 올려줄 수 없기떄문에
부모의 데이터를 바꾸기 위해서는 state를 이용해야 한다.

3️⃣ **Props and State**

- **Props**: 부모 컴포넌트에서 자식 컴포넌트로 전달해주는 데이터.   
자식 컴포넌트에서 전달 받은 props는 변경이 불가능하고  
props를 전달해준 최상위 부모 컴포넌트만 props를 변경할 수 있다.

- **State**: 사용자와의 상호작용을 통해 데이터를 동적으로 변경해야 하는 것과 같이 동적인 데이터를 다룰 때 사용한다.  
state를 변경해주는 함수를 props로 받는다면 state의 변경이 가능하다.


<HR>

####  참고자료
- [Frontend 기술 면접 대비 React 와 Vue](https://velog.io/@wngkdroqkf441/Frontend-%EA%B8%B0%EC%88%A0-%EB%A9%B4%EC%A0%91-%EB%8C%80%EB%B9%84-React%EC%99%80-Vue)
- [Vue.js란 무엇인가?](https://ko-seung.tistory.com/45)
- [리액트(React.js) vs 뷰(Vue.js)](https://nyol.tistory.com/148)
- [내가 REACT를 선택한 이유](https://helloworld-88.tistory.com/350)
