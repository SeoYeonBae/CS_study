# :pushpin: OAuth


## :computer: OAuth란?

:heavy_check_mark:  OAuth의 등장 배경

- 구글의 캘린더에 일정을 추가하거나, 페이스북, 트위터에 글을 남기는 기능을 구현하고 싶다??!!
- 이때, 가장 쉽게 이 기능을 구현하는 방법은 사용자로부터 구글, 페이스북, 트위터의 **ID, Password**를 직접 제공받아 우리의 서비스에 저장하고 활용하는 방법

    ![image](https://user-images.githubusercontent.com/69101568/235347927-9282f29a-76be-4821-b73a-61f020f26dfc.png)
_대충 이런 흐름_

- 하지만 이 방법은 보안상 안전하지 않음
- 사용자의 구글, 페이스북, 트위터 ID, Password의 **탈취 위험성**이 있음

:heavy_check_mark: OAuth란?

- 구글, 페이스북, 트위터와 같은 다양한 플랫폼의 특정한 사용자 데이터에 접근하기 위해 제 3자 클라이언트가 사용자의 **접근 권한을 위임 받을 수 있는 표준 프로토콜**
- 우리의 서비스가 타사 플랫폼 정보에 접근하기 위해서 권한을 타사 플랫폼으로부터 위임 받는 것

---

## :computer: OAuth 2.0 주체

:heavy_check_mark: Resource Owner
- 자원의 소유자
- Client가 제공하는 서비스를 통해 로그인하는 실제 유저

:heavy_check_mark: Resource Server
- Client가 제어하고자 하는 자원을 보유하고 있는 서버
- Facebook, Google, Twitter 등

:heavy_check_mark: Client
- Resource Server에 접속해서 정보를 가져오고자 하는 클라이언트(웹 어플리케이션)

---

## :computer: 어플리케이션 등록

:heavy_check_mark: Client ID
- 클라이언트 웹 어플리케이션을 구별할 수 있는 식별자
- 노출되어도 상관 없음

:heavy_check_mark: Client Secret
- Client ID에 대한 비밀키
- 절대 노출되어서는 안됨

:heavy_check_mark: Authorized Redirect URI
- Authorization Code를 전달받을 리다이렉트 주소
- 등록되지 않은 redirect URI을 사용하는 경우, code를 중간에 탈취당할 위험성이 있기 때문에 Resource Server가 인증을 거부함

---

## :computer: OAuth 2.0의 동작 메커니즘

![image](https://user-images.githubusercontent.com/69101568/235349200-746beb65-41f3-4b8d-b5d7-aa45c4f29fd0.png)

:heavy_check_mark: 1~2. 로그인 요청
- Client는 Authorization Server가 제공하는 Authorization URI에 `response_type`, `client_id`, `redirect_uri`, `scope` 등의 매개변수를 쿼리 스트링으로 포함하여 보냄
    ```
    https://authorization-server.com/auth?response_type=code
    &client_id=29352735982374239857
    &redirect_uri=https://example-app.com/callback
    &scope=create+delete
    ```

:heavy_check_mark: 3~4. 로그인 페이지 제공, ID/PW 제공
- Authorization URI로 이동된 Resource Owner는 제공된 로그인 페이지에서 ID와 PW 등을 입력하여 인증

:heavy_check_mark: 5~6. Authorization code 발급, Redirect URI로 리다이렉트
- 인증이 성공이 되면, Authorization Server는 Authorization code를 포함하여 제공된 Redirect URI로 사용자를 리다이렉트
- 이 때, Authorization code는 수명이 짧음

:heavy_check_mark: 7~8. Authorization code와 Access Token 교환
- Client는 Authorization Server에 code를 전달하고 Access Token을 응답 받음
- Access Token은 유출되어서는 안되기 때문에 **HTTPS 연결**을 통해서만 사용 가능

:heavy_check_mark: 9. 로그인 성공
- 위 과정을 성공적으로 마치면 Client는 Resource Owner에게 로그인이 성공하였음을 알림

:heavy_check_mark: 10~13. Access Token으로 리소스 접근
- 이후 Resource Owner가 Resource Server의 리소스가 필요한 기능을 Client에 요청
- Client는 Access Token을 사용하여 제한된 리소스에 접근하고, Resource Owner에게 자사의 서비스를 제공

---

<br>

참고

- [OAuth 2.0 개념과 동작원리](https://hudi.blog/oauth-2.0/)
- [OAuth 개념 및 동작 방식 이해하기](https://tecoble.techcourse.co.kr/post/2021-07-10-understanding-oauth/)