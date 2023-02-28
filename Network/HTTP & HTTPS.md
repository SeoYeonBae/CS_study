# 🌏 HTTP & HTTPS

## 1️⃣ HTTP (Hyper Text Transfer Protocol)

  
- 서버와 클라이언트간에 데이터를 주고 받는 프로토콜  
- 서버에서 브라우저로 전송되는 정보가 암호화되지 않는 보안적 허점  

<br>
<br>

   
### 🛫 HTTP의 동작 과정

1. 사용자가 웹 브라우저에 URL주소 입력
2. DNS 서버에 웹 서버의 호스트 이름을 IP주소로 변경 요청
3. 웹 서버와 TCP 연결 시도 **( 3 way-handshaking )**
4. 클라이언트가 서버에게 요청

![image](https://user-images.githubusercontent.com/63834758/221482278-cab3ed7a-9f0c-49e5-9bc9-28143167a199.png)

    - HTTP Request Messag = Request Header + 빈 줄 + Request Body
    - Request Header
       ( 요청 메소드 + 요청 URI + HTTP 프로토콜 버전 )
        - GET /background.png HTTP/1.0 POST / HTTP 1.1
        - Header 정보(key-value 구조)
    - 빈 줄
        - 요청에 대한 모든 메타 정보가 전송되었음을 알리는 용도
    - Request Body
        - GET, HEAD, DELETE, OPTIONS처럼 리소스를 가져오는 요청은 바디 미포함 
        - 데이터 업데이트 요청과 관련된 내용 (HTML 폼 콘텐츠 등)
  
  
5. 서버가 클라이언트에게 데이터 응답

![image](https://user-images.githubusercontent.com/63834758/221720222-65358d24-e7e4-47b8-b7f1-5480c9522681.png)

    - HTTP Response Message = Response Header + 빈 줄 + Response Body
    - Response  Header
       ( HTTP 프로토콜 버전 + 응답 코드 + 응답 메시지 )
        - HTTP/1.1 404 Not Found.
        - Header 정보(key-value 구조)
    - 빈 줄
        - 요청에 대한 모든 메타 정보가 전송되었음을 알리는 용도
    - Request Body
        - 응답 리소스 데이터 
        - 201, 204 상태 코드는 바디 미포함
        
6. 서버 클라이언트 간 연결 종료 **( 4 way-handshaking )**
7. 웹 브라우저가 웹 문서 출력
  

<br>
<br>

## 2️⃣ HTTPS (Hyper Text Transfer Protocol Secure)
  
- HTTP에 **데이터 암호화**가 추가된 프로토콜
- **SSL(보안 소켓 계층)** 로 암호화된 연결 형성
- **TLS(전송 계층 보안)** 프로토콜로 보안 유지
    - 데이터 무결성 보장
    - 데이터 전송 중 수정 및 손상 방지
- 참고 : [SSL/TLS](https://github.com/SeoYeonBae/CS_study/blob/main/Network/TLS%26SSL%20HandShake.md)


 
<br>

### 🛫 HTTPS의 동작 과정

- 대칭키 **암호화 & 비대칭키** 암호화 모두 사용 👉 빠른 연산 속도 & 안정성

- 처음 연결을 성립하여 안전하게 세션키를 공유하는 과정 👉 **비대칭키 사용**
- 이후 데이터 교환하는 과정에서 빠른 연산 속도를 위해 👉 **대칭키(세션키) 사용**  
  
  
1. 브라우저(클라이언트) : 서버로 최초 연결 시도  
3. 서버 : ***공개키(엄밀히는 인증서)를*** 브라우저에게 넘겨줌
4. 브라우저 : 인증서의 유효성 검사 👉 ***세션키 발급***
5. 브라우저 : 세션키 보관 + 추가로 서버의 공개키로 ***세션키를 암호화*** 👉 서버로 전송
6. 서버 : 개인키로 암호화된 ***세션키를 복호화*** 👉 세션키 획득
7. 클라이언트와 서버는 동일한 세션키를 공유하므로 데이터를 전달할 때 ***세션키로 암호화/복호화*** 를 진행함

 ![image](https://user-images.githubusercontent.com/63834758/221483730-a07d795d-3859-4918-8140-4633632b293e.png)


<hr>


#### 참고자료

- [HTTP와 HTTPS의 개념 및 차이점](https://mangkyu.tistory.com/98)
- [인터넷 프로토콜 http와 https의 차이](https://post.naver.com/viewer/postView.nhn?volumeNo=16561296&memberNo=1834)
- [HTTP와 HTTPS의 동작과정](https://jiyoungtt.tistory.com/66)
