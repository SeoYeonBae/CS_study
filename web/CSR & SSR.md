# CSR & SSR
- 브라우저 렌더링
- SPA & MPA
- CSR
- SSR
- CSR과 SSR의 차이


<br>

## 브라우저 렌더링
- 브라우저(클라이언트)가 서버에 요청하고 응답받은 내용을 브라우저 화면에 표시해주는 작업
- **CSR**과 **SSR** 방식 존재

<br>

### *⏹️ 브라우저 렌더링 방식을 보기 전에!⏹️*
<br>


## SPA & MPA
### SPA *(Single Page Application)*
- 하나의 페이지로 이루어진 홈페이지
- 페이지에 필요한 모든 정적 리소스를 최초 한 번에 다운로드한다. 
- 이후 새로운 페이지 요청이 있을 때, 페이지 갱신에 필요한 데이터만 전달받아 페이지 갱신
- 데이터 수정, 조회 시 동적으로 페이지를 구성하기에 페이지가 새로고침되지 않고, 다른 페이지로 넘어가지 않음
- CSR에 적합 (주의! SPA 방식이 모두 CSR인 것은 아니다.)
- Vue, Angular, React로 만든 홈페이지들이 대부분 SPA에 속함


### MPA *(Multiple Page Application)*
- 여러 개(Single)의 페이지로 이루어진 홈페이지
- 페이지 이동할 때마다 클라이언트에서 서버로 요청을 보내면 서버에서 렌더링하고 클라이언트에게 응답을 보내는 SSR 환경 사용
- 페이지 이동하거나 새로고침하면 전체 페이지 다시 렌더링한다.
- React를 서버사이드에서 렌더링하고 싶은 경우 Next.js 사용

<br>

## CSR
- _Client Side Rendering_
- 렌더링이 클라이언트 쪽에서 일어난다.
- 서버는 요청을 받으면 클라이언트에게 HTML과 JS를 보내주고, 클라이언트는 이를 받아 렌더링을 시작한다.

### 🔄 작동 과정
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/91e57bf5-95fe-4fc8-b43f-fb2765eb36ef)
1. User가 Website 요청을 보낸다.
2. CDN이 JS로 접근할 수 있는 링크를 포함한 HTML을 클라이언트에게 보낸다. *(CDN : Content Delivery Network, 데이터 사용량이 많은 애플리케이션의 웹 페이지 로드 속도를 높이는 상호 연결된 서버 네트워크)*
3. 클라이언트(브라우저)가 HTML와 JS를 다운로드 받는다. **이때, User는 아무것도 볼 수 없다.**
4. 클라이언트(브라우저)가 JS를 다운로드 받는다.
5. 클라이언트(브라우저)가 JS 프레임워크를 실행한다. 데이터를 위한 API가 호출되고 이때 User는 placeholder를 보게된다. (빈 화면: 비어있는 HTML 받았기 문)
6. Server는 API 요청에 data로 응답한다.
7. API로부터 받은 data를 placeholder에 채워넣고, 웹 페이지 내에서 상호작용이 가능해진다.

*즉, JS가 모두 다운로드되고 실행이 끝나기 전까지 User는 페이지를 볼 수 없다.*
> - 브라우저가 화면을 렌더링하기에 서버 트래픽이 감소하고, User에게 더 빠른 인터렉션을 제공함
> - 새로고침이 발생하지 않아 User가 네이티브 앱과 비슷한 경험을 할 수 있음
<br>

## SSR

- _Server Side Rendering_
- 서버족에서 렌더링 준비를 끝마친 상태로 클라이언트에 전달한다.
- 클라이언트에서 서버에 데이터를 요청할 때마다 새로운 화면을 만들어 제공한다.

### 🔄 작동 과정
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/fa8a32c8-7afa-4dcb-b0c7-f7b0156518b8)

1. User가 Website 요청을 보낸다.
2. Server가 'Ready to Render'. 즉, 즉시 렌더링 가능한 HTML 파일을 만든다. (리소스 체크, 컴파일 후 완성된 HTML 만든다.)
3. 클라이언트에 전달하는 순간, 이미 렌더링 준비가 되어있기 때문에 HTML 즉시 렌더링되지만 JS 읽히기 전이기에 사이트 자체 조작(interactive)은 불가능하다.
4. 클라이언트(브라우저)가 JS를 다운로드 받는다.
5. 다운로드 받는 동안 User는 컨텐츠를 볼 수 있지만 조작할 수 없지만 이때의 사용자 조작을 기억하고 있는다.
6. 클라이언트(브라우저)가 JS 프레임워크를 실행한다.
7. JS가 성공적으로 컴파일되었기에 기억하고 있던 사용자 조작이 실행되고, 웹 페이지 내에서 상호작용이 가능해진다.

*즉, JS가 다운로드 되는 동안 User는 무언가를 보고 있을 수 있다.*
> - 클라이언트(브라우저)가 서버에 매번 데이터를 요청하고, 서버에서 처리하는 방식
> - 검색 엔진 최적화(SEO: 검색 엔진에서 찾기 쉽도록 사이트를 개선하는 프로세스) 가능
<br>

## CSR과 SSR의 차이

### 웹 페이지 로딩 시간
- 웹 페이지 로딩은 웹 사이트의 가장 **첫 페이지 로딩**과 **나머지**를 로딩하는 것으로 나뉜다.
- 첫 페이지 로딩 시간


|CSR|SSR|
|---|---|
|HTML과 모든 스크립트들을 한 번에 불러온다.|필요한 부분의 HTML과 스크립트를 불러온다.|
|느림|빠름|


- 나머지 로딩 시간
  - 첫 페이지 로딩 후, 사이트의 다른 곳으로 이동한다고 가정


|CSR|SSR|
|---|---|
|첫 페이지 로딩할 때 모든 스크립트들을 한 번에 불러온 상태|필요한 부분의 HTML과 스크립트를 불러온다.|
|빠름|느림|


### SEO 대응
- _Search Engine Optimization : 검색 엔진 최적화_

|CSR|SSR|
|---|---|
|웹 사이트에 대한 데이터 수집을 제대로 못하는 경우가 발생할 수 있음 : 초기 HTML 파일 비어있기 때문|서버에서 컴파일되어 클라이언트로 넘어오기에 크롤러에 대응 용이|
|별도의 보완 작업 필요|가능|

<br>

### 서버 자원 사용
    
|CSR|SSR|
|---|---|
|HTML과 모든 스크립트들을 한 번에 불러온다.|필요한 부분의 HTML과 스크립트를 불러온다.|
|느림|빠름|

<hr>


### 참고자료

- [SSR과 CSR의 차이](https://proglish.tistory.com/216)
- [CSR과 SSR의 장단점](https://www.startupcode.kr/company/blog/archives/12)