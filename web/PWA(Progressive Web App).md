# :pushpin: PWA(Progressive Web App)


## :iphone: PWA란?

_HTML, CSS, 자바스크립트와 같은 웹 기술들을 사용해 만드는 앱_

        - Uber
        - Starbucks
        - Google Developers
        - Pinterest
        - Twitter...

:heavy_check_mark: PWA의 배경

- 2015년 구글 크롬의 엔지니어 알렉스 러셀이 처음으로 사용
- 차세대 웹의 개념으로써 점진적으로 네이티브 앱 수준으로 근접해가는 웹
- 웹이지만 데스크톱이나 모바일 환경에 설치가 가능하고 앱과 유사한 사용자 경험을 제공해주는 웹 앱을 제공하고자 하는 시도이자 방법론!

:heavy_check_mark: PWA 조건

- 사용자의 기기에 설치가 가능할 것 (브라우저 탭이 아닌 독립 실행형 창으로 열릴 것)
- 오프라인, 저속도 환경에서도 동작할 것
- 백그라운드 동기화가 가능할 것
- 사용자 재참여를 유도할 수 있도록 푸시 알림이 가능할 것
- 다양한 Web API를 사용하여 네이티브 앱과 같은 사용성을 갖출 것 (사용자 위치, 카메라 등)
- HTTPS 프로토콜을 통해 제공할 것 (보안, 안정성)

**구글이 PWA라는 기술을 새롭게 개발한 것이 아니라 방법론과 개념으로써 PWA를 제시하고 자신의 브라우저인 크롬에 최신 Web API를 접목시키고 확장하려는 것이라는 게 포인트!**

---

## :iphone: PWA가 될 수 있게 하는 필수 요소

_PWA가 새롭게 개발된 프로그래밍 언어나 프레임워크가 아니기 때문에 기존에 존재하는 일반 웹도 PWA로 전환이 쉽게 가능하다_

:one: Web App Manifest JSON 파일

- 브라우저에게 PWA에 대한 메타 정보와 현재 웹 사이트가 유저의 데스크톱이나 모바일 장치에 어떻게 설치되어야 하는지에 대한 정보를 저장한 파일
- 앱 이름, 아이콘, 테마 색상 정보 등을 포함

:two: 서비스워커.js
- PWA의 핵심 기능인 푸시 알림, 백그라운드 동기화, 오프라인 환경 지원, 리소스 캐싱의 구현체를 담을 수 있는 스크립트 파일
- JavaScript 기반의 Web API의 한 종류로 브라우저의 백그라운드에서 독립된 스레드 실행 -> 백그라운드 실행 가능

:three: 아이콘 이미지 파일

:four: HTTPS

---

## :iphone: PWA의 장점

:heavy_check_mark: 앱 개발 생산성 극대화

- 네이티브에 대한 기술이 전혀 요구되지 않는 하나의 코드 베이스
- 익숙한 웹 기술 (HTML, CSS, JS)을 이용하여 다양한 플랫폼에서 동작하는 설치형 앱을 빠르게 만듦

:heavy_check_mark: 검색 엔진을 통한 유입

- 본질적으로는 웹이기에 검색 가능
- 사용자 유입 가능성 증가

:heavy_check_mark: 푸시 알림

- 네이티브 앱만이 가지고 있던 푸시 알림이 PWA에서도 가능
- 푸시 알림을 통해 사용자 재참여 유도 (iOS는 최근 16.4부터 지원)

:heavy_check_mark: 저속도 네트워크 환경, 오프라인 동작 지원

- 서비스 워커 덕분에 앱 동작에 필요한 asset들과 일부 API call에 대한 캐싱이 가능
- 안정적인 앱 사용 지원

---

## :iphone: PWA의 단점과 한계

:heavy_check_mark: PWA에 대한 인지도 부족, 앱 설치의 애매함

- 앱 스토어를 통해 앱을 설치해야 안전하다는 인식을 가진 일반 사용자들에게 낯선 방식

:heavy_check_mark:  Non-native UI

- 네이티브 앱만큼 각 운영체제 고유의 UI와 사용자 경험을 제공할 수 없음

:heavy_check_mark: Apple의 소극적인 지원

- 개발자와 사용자들이 Apple의 앱스토어를 통하지 않고 자유롭게 앱을 만들고 사용하면 앱 수수료라는 수익원을 포기하게 됨 
- 그래서 Apple은 지금까지 PWA에 대해 엄청 소극적이었음
- 최근에서야 웹 푸시 알림 기능을 포함한 iOS의 업데이트가 있었음

:heavy_check_mark: 게임과 같은 고사양 앱 개발 불가능

- 운영체제의 자원을 직접적으로 사용할 수 있는 네이티브 앱보다 퍼포먼스가 낮음
- 높은 연산을 요구하는 작업, 그래픽 사용이 필수인 게임 앱 개발에는 한계가 있음

---

<br>

참고

- [앱 개발 “PWA(Progressive Web Application)” 정의/요소/장단점/사례/트위터 예시](https://www.sepoasoft.co.kr/?p=7411)