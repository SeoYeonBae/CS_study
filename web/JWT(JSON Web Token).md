# JWT (JSON Web Token)
- JSON 객체를 사용해서 토큰자체에 정보들을 저장하고 있는 Web Token
- 유저를 인증하고 식별하기 위한 토큰 기반 인증


## 1. 핵심 특징
- 토큰 자체에 사용자의 권한 정보 or 서비스를 사용하기 위한 정보가 포함(Self-contained)된다
- 따라서, 토큰에 저장되는 정보가 많아지면 네트워크 사용량 증가

## 2. JWT 동작 절차


1 클라이언트(사용자)가 ID, PW를 통해 서버에 인증을 요청(ex. 로그인)
2 서버에서 서명된(Signed) JWT를 생성하여 클라이언트로 반환
3 클라이언트는 서비스를 사용하기 위해 인가가 필요할 때 서버로부터 반환받은 JWT를 HTTP 헤더에 첨부하여 요청
4 서버는 클라이언트로부터 수신받은 HTTP 헤더의 JWT를 검증한 후, 요청을 처리

## 2. JWT의 구조
JHeader, Payload, Signature로 구성

### Header

JWT에서 사용할 타입과, Signature를 해싱하기 위한 해시 알고리즘의 종류를 포함

### Payload

서버와 클라이언트가 주고받는, 즉 시스템에서 실제로 사용되는 정보들을 포함
서버에서 첨부한 사용자 권한 정보, 데이터를 포ㅎㅏㅁ

### Signature

토큰의 유효성 검증을 위한 문자열
Header, Payload를 Base64 URL-safe Encode 한 후, Header에 명시된 해시함수를 적용하고, 개인키(Private Key)로 서명한 전자서명을 포함
해당 전자서명은 Header와 Payload가 변조되었는지를 확인하기 위해 사용되며, 이를 통해 JWT의 신뢰성을 증명
