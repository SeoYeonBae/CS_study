# 💫 Fragment와 React Hook
 

## 1️⃣ Fragment
  
  
하나의 컴포넌트에서 여러 개의 요소를 반환하기 위해서 최상위 태그로 무조건 감싸야한다.

하지만 React.Fragments ( Fragment 또는 빈칸 )로 별도의 노드 추가 없이 컴포넌트를 생성 가능.

### (1) 사용 이유
  ```
// App.js
const App = () => {
  return (
    <UserForm />
  );
};

// UserForm.js
const UserForm = () => {
  return (
    <div>
      <form>
        <label>Username</label>
        <button type="submit">Add User</button>
      </form>
      <aside>
        <h1>modal</h1>
      </aside>
    </div>
  );
};
```

**form과 aside를 감싸는 div**
- 여러가지 요소를 감싸는 것 외에 아무런 기능을 하지 않는다.
- 이런 태그는 스타일링 작성 시 방해가 되며, 많은 요소를 렌더링하면서 application이 느려질 수 있다.

### (2) 사용 방법

- 리액트에서 제공하는 Fragment를 import하여 태그에 지정해 사용한다.
- <React.Fragment>대신 <Fragment>, <>도 사용 가능

```
// UserForm.js
import React from 'react';
const UserForm = () => {
  return (
    <React.Fragment>
      <form>
        // 중략
      </form>
      <aside>
        // 중략
      </aside>
    </React.Fragment>
  );
};
```


## 2️⃣ React Hook

React 16.8버전에 새로 추가된 기능으로 state, component에 대한 것들을 바꿔놓았다.


- 리액트 컴포넌트는 **클래스형 컴포넌트(Class Component)** 와 **함수형 컴포넌트(Functional Component)** 로 나뉜다.
- 기존 : 함수형 컴포넌트를 주로 사용 & state이나 Life Cycle method를 사용해야 할 때에만 클래스형 컴포넌트를 사용

- react hook로 만든 앱 : class component, render 등을 안해도 된다.
    - **function component에서 state을 가질 수 있다.**
    - 모든 것은 하나의 function이 된다. (**함수형 프로그래밍이 가능**해지는 것) 


### (1) 사용 이유 

클래스형 컴포넌트가 가지는 단점 때문

**1. 길고 복잡한 코드**

constructor, this, binding 등 지켜야 할 규칙이 많아서 코드가 복잡하고 길다.  

JAVA처럼 OOP(Object-oriented programming)의 테크닉을 수려하게 적용하지는 않으면서도 근본은 클래스의 모습을 띄고 있기 때문이다.

<br>
 
**2. Logic 재사용 어려움**

클래스형 컴포넌트에서는 High-Order Components(HOC)로 컴포넌트 자체를 재사용 할 수는 있지만  
부분적인 DOM 관련 처리나 API사용 및 state을 다루는 등의 logic에 있어서는  
경우에 따라 같은 로직을 2개 이상의 Life Cycle method에 중복해서 넣어야하는 등 재사용에 제약이 따른다.

이에 반해 hooks를 활용한 함수형 컴포넌트 = **원하는 기능을 함수로 만든 후(hook) 필요한 곳에 훅 집어 넣어주기만 하면 된다**

<br>

**3. 성능**

리액트 측에서 2015년 10월에 향후 함수형 컴포넌트의 performance를 상승시킬것이라고 발표했고,  
대략 6% ~ 45% 상승했다고 말한다.

 
<br>
<br>

이러한 단점들에도 불과하고, 그동안 클래스형 컴포넌트를 사용했던 이유 state관리와 Life cycle method의 사용때문이었다.  

복잡하고 뚱뚱하지만, 클래스의 힘을 빌려야만 React가 원활하게 작동할 수 있었다.  

그런데 hooks의 등장으로 인해 함수형 컴포넌트에서도 이러한 클래스형 컴포넌트의 작업들을 할 수 있게 되었다.




  <hr>

#### 참고자료
- [Fragment 사용하는 이유와 방법](https://velog.io/@yeonsubaek/React-Fragment-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0%EC%99%80-%EC%82%AC%EC%9A%A9-%EB%B0%A9%EB%B2%95)
- [React Hooks란](https://studyingych.tistory.com/59)
- [리액트 훅(react hook)이란? - 클래스형 컴포넌트와 비교](https://codingbroker.tistory.com/23)


        
