# Vue.js 라이프사이클

인스턴스 or 컴포넌트가 생성되고 사라지기까지 거치는 단계들.  
'우리 눈에 보여지고 사라지기까지의 단계'를 일컫는 말



- 라이프사이클 : 인스턴스의 상태에 따라 호출할 수 있는 속성들
- 라이프사이클 훅 : 그 속성마다 개발자가 추가한 커스텀 로직


## 👩🏻‍💻 흐름도
![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/e5090d56-1b6c-4baa-be7b-61c49fb2e415)


크게 4단계로 나누면
1. 인스턴스의 생성 (create)
2. 생성된 인스턴스를 화면에 부착 (mount)
3. 화면에 부착된 인스턴스의 내용 갱신 (update)
4. 인스턴스가 소멸 (destroy)

<br>
     
  
### 🍀 beforeCreate
- 인스턴스가 생성되고 나서 **가장 처음으로 실행되는** 라이프 사이클 단계
- 인스턴스 초기화 직후, 데이터 관찰 및 이벤트/감시자(watcher) 설정 전에 동기적으로 호출됨  
- 뷰 인스턴스의 data와 methods 속성이 정의되어 있지 않아서 **화면 요소(dom)에 접근 불가**

<br>

### 🍀 created
- data 관찰, computed 속성, methods, watch/이벤트 콜백 등의 설정이 활성화되어 접근이 가능하다.
- data, methods 속성이 정의되어서 **data에 접근 가능!**
- 컴포넌트 초기에 외부에서 받아온 값들을 data로 세팅해야할 때 필요한 단계

- ⚠️ 하지만 mount 단계가 시작되지 않았으므로, $el 속성 사용 불가.  
화면 요소가 인스턴스에 부착되기 전이므로 template 속성에 정의한 DOM 요소에 접근하는 코드를 구현할 수 없음

<br>

### 🍀 beforeMount

- 가상 DOM은 이미 생성되었으나, 실제 DOM에 부착하기 직전에 호출됨
- render 함수(js로 DOM을 그리는 함수)가 처음으로 호출되기 직전의 단계이므로, **인스턴스를 화면에 붙이기 전 실행해야 할 코드를 구현**

<br>

### 🍀 mounted
- 가상 DOM의 내용이 실제 DOM에 부착된 이후에 실행되는 훅
- $el을 사용하여 실제 DOM에 접근 가능 == **화면 요소를 제어하는 로직 수행하기 좋은 단계**
- ⚠️ 하지만 모든 자식 컴포넌트가 mount되었다고 할 수는 없다.
    - 돔에 인스턴스가 부착되자마자 호출되기 때문에, 하위 컴포넌트나 외부 라이브러리에 의해
후에 추가된 화면 요소들은 최종 HTML 코드로 변환되는 시점과 다를 수 있음
    - 전체 렌더링이 된 상태에서 작업을 진행하려면 $nextTick 사용

<br>

### 🍀 beforeUpdate
- 컴포넌트에서 사용하는 data의 값이 변경되면 컴포넌트가 재렌더링 수행.  
그때 가상 DOM으로 화면을 다시 그리기 전에 호출되는 단계
- 변경 예정인 data 값을 이용해 작업을 해야할 때 적절한 단계
    - ex : 화면 요소에 인스턴스가 부착된 후, $watch 속성으로 관찰하던 데이터가 변경되면 가상 DOM을 이용해 화면에 다시 그려지게 될 때

<br>


### 🍀 updated

- 데이터가 변경되어 가상 DOM이 다시 화면을 그리고 나면 실행되는 단계

- ⚠️ update 단계에서 data를 수정하면, 또 update 훅이 호출되므로 무한 루프에 빠질 수 있다.

    - updated 훅 내부에서 DOM의 종속적인 연산을 할 순 있지만, 상태 변경에 반응하기 위해 computed나 watch 를 사용하는 것이 좋다

    - beforeUpdate -> updated (또 값 변경) -> beforeUpdate -> updated ...

    - 데이터 값을 갱신하는 로직은 beforeUpdate에서 처리하자

- ⚠️mounted와 마찬가지로 모든 하위 컴포넌트가 다시 렌더링 되었음을 보장하지 않는다.
    - $nextTick을 사용해 전체 화면이 재렌더링 될 때까지 기다릴 수 있음

<br>

### 🍀 beforeUnmount
- 컴포넌트 인스턴스가 mount 해제 되기 직전에 호출, 아직 인스턴스는 완전하게 동작
- 인스턴스가 사라지기 직전 해야하는 작업 구현

### 🍀 unmounted
- 컴포넌트 인스턴스가 mount 해제된 후 호출
- 모든 디렉티브가 바인딩 해제되고, 이벤트 리스너가 제거되며, 모든 자식 컴포넌트도 마운트 해제




<hr>

#### 참고자료
- [Vue.js 라이프사이클](https://velog.io/@uoayop/Vue.js-%EB%9D%BC%EC%9D%B4%ED%94%84-%EC%82%AC%EC%9D%B4%ED%81%B4)
- [Vue.js 시작하기 - 라이프사이클](https://developerjournal.tistory.com/5)
