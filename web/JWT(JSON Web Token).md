# JWT (JSON Web Token)
- **JSON 객체**를 사용 👉 토큰 자체에 정보들을 저장하고 있는 **Web Token**
- 유저를 인증 & 식별하기 위한 **토큰 기반 인증**


<br>

## 1. 핵심 특징
- 토큰 자체에 _사용자의 권한 정보_ or _서비스를 사용하기 위한 정보_ 가 포함(Self-contained)된다
- 따라서, 토큰에 저장되는 정보 ↑ = 네트워크 사용량 ↑

<br>

## 2. JWT의 구조

- JWT는 각각의 구성요소가 점(.)으로 구분이 되어있으며 구성 요소는 다음과 같다.

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/16169a7d-e3c2-4377-b332-154b13f2c52b)


### 1️⃣ Header
![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/5e0e9f79-477e-4818-868f-0443ee15e984)

JWT에서 사용할 타입 & Signature를 해싱하기 위한 해시 알고리즘의 종류를 포함

### 2️⃣ Payload
![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/dad42631-db13-4cad-a369-1fd60d6f4a63)

서버와 클라이언트가 주고받는, 즉 시스템에서 실제로 사용되는 정보들을 포함
서버에서 첨부한 사용자 권한 정보, 데이터를 포함

### 3️⃣ Signature
![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/9b0e9bab-f4f3-4464-9e0c-3069f902b665)

토큰의 유효성 검증을 위한 문자열
Header, Payload를 Base64 URL-safe Encode 한 후, Header에 명시된 해시함수를 적용하고, 개인키(Private Key)로 서명한 전자서명을 포함
해당 전자서명은 Header와 Payload가 변조되었는지를 확인하기 위해 사용되며, 이를 통해 JWT의 신뢰성을 증명

<br>

## 3. JWT 동작 절차


1️⃣ **클라이언트(사용자)** : ID, PW를 통해 서버에 인증 요청(ex. 로그인)  
2️⃣ **서버** : 서명된(Signed) JWT를 생성하여 클라이언트로 반환  
3️⃣ **클라이언트** : 서비스를 사용하기 위해 인가가 필요할 때 서버로부터 반환받은 JWT를 HTTP 헤더에 첨부하여 요청  
4️⃣ **서버** : 클라이언트로부터 수신받은 HTTP 헤더의 JWT를 검증한 후, 요청을 처리

<br>

## 4. 장점

- 이미 토큰 자체가 인증된 정보이기 때문에 세션 저장소와 같은 별도의 인증 저장소가 "필수적"으로 필요하지 않다.

- 세션과는 다르게 클라이언트의 상태를 서버가 저장해 두지 않아도 된다.

- signature를 공통 키 개인키 암호화를 통해 막아두었기 때문에 데이터에 대한 보완성 ↑

- 다른 서비스에 이용할 수 있는 공통적인 스펙으로써 사용 가능

<br>

## 5. 요약

stateful 해야 하는 세션의 단점을 보완하기 위해 만들어진 JWT는  
별도의 세션 저장소를 강제하지 않기 때문에 stateless 하여 확장성이 뛰어나고,  
signature를 통한 보안성까지 갖추고 있다.



<hr>

### 참고자료

- [JWT (Json Web Token) 이란?](https://velog.io/@corone_hi/JWT-Json-Web-Token-%EC%9D%B4%EB%9E%80)
- [JWT - Json Web Token](https://www.daleseo.com/jwt/)
