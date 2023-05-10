# 🔰 JWT (JSON Web Token)
- **JSON 객체**를 사용 👉 토큰 자체에 정보들을 저장하고 있는 **Web Token**
- 유저를 인증 & 식별하기 위한 **토큰 기반 인증**

- 공개/개인 키를 쌍으로 사용하여 토큰에 서명할 경우  
    이 서명된 토큰이 정상적인 토큰인지를 서버가 확인할 수 있다. (개인키를 보유한 서버)

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

- JWT 토큰에서 사용할 타입 & Signature를 해싱하기 위한 해시 알고리즘의 종류를 포함
    - 토큰 타입이 JWT라는 의미
    - HS512 개인키 알고리즘을 적용하여 암호화했다는 의미

### 2️⃣ Payload
![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/dad42631-db13-4cad-a369-1fd60d6f4a63)

- 서버와 클라이언트가 주고받는, 즉 시스템에서 실제로 사용되는 정보들을 포함
- 보통 Claim이라는 사용자 or 토큰에 대한 property를 key-value 형태로 저장
    - Claim : 말 그대로 토큰에서 사용할 정보의 조각
- 표준 스펙 상 key의 이름은 3글자 ( 토큰에 대한 표현 압축)
    - _iss (Issuer)_ : 토큰 발급자
    - _sub (Subject)_ : 토큰 제목 (사용자에 대한 식별 값)
    - _aud (Audience)_ : 토큰 대상자
    - _exp (Expiration Time)_ : 토큰 만료 시간
    - _nbf (Not Before)_ : 토큰 활성 날짜 (이 날짜 이전의 토큰은 활성화 되지않음을 보장)
    - _iat (Issued At)_ : 토큰 발급 시간
    - _jti (JWT Id)_ : JWT 토큰 식별자 (issuer가 여럿일 때 구분하기 위한 값)

> 이렇게 정의되어 있는 Claim 스펙이 있다는 것이지,
> 
> 꼭 이 7가지를 모두 포함해야 하는 것은 X
> 
> 상황에 따라 해당 서버가 가져야할 인증 체계에 따라 사용하면 된다.

> 표준 스펙 외에도 필요한 정보를 개발자가 원하는대로 추가 가능
> 
> 예시 ) "token_type" : "access token"

- 다만 주의사항은 **Payload에 민감한 정보를 담지 않는 것이다.**
    - headerd와 payload는 json이 디코딩되어있을 뿐, 특별한 암호화 X
    - 그러므로 단순히** "식별하기 위한" **정보만을 담아두어야 한다.
    - 서버에서 생성한 JWT를 jwt.io 사이트에 넣기만 해도 아래처럼 정보를 볼 수 있다.
    ![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/c98f255d-554f-4865-a2da-c8608ae2c04c)

- header, payload가 식별값만 존재하더라도 암호화가 필요하지 않은가?
    - 사실 필요없는 행위이다. 암호화 자체가 많은 리소스를 사용한다.
    - 매 http 요청마다 1번의 복호화가 더 추가되는 셈이기 때문이다.


### 3️⃣ Signature

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/9b0e9bab-f4f3-4464-9e0c-3069f902b665)

- 가장 중요한 서명
- header를 디코딩한 값, payload를 디코딩한 값을 위 사진 처럼 합치고,  
이를 your-256-bit-secret 즉, **서버가 가지고 있는 개인키를 가지고 암호화되어있는 상태**이다.  
- 따라서 signature는 **서버에 있는 개인키로만 암호화를 풀 수 있으므로**  
다른 클라이언트는 임의로 Signature를 복호화할 수 없다.


> (1) JWT 토큰을 클라이언트가 서버로 요청과 동시에 전달한다.
> 
> (2) 서버가 가지고 있는 개인키를 가지고 Signature를 복호화한 다음 
> 
> (3) base64UrlEncode(header)가 JWT의 heaer값과 일치한 지,  base64UrlEncode(payload) 와 일치한 지 확인하여 <br>
> 일치한다면 인증을 허용한다.
> 
> (4) 만약 클라이언트가 payload에 담긴 식별자가 변조된 JWT로 요청을 하더라도  
서버가 애초에 발급했던 Signature 안의 payload와 다르기 때문에 인증이 불가능해진다.

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
