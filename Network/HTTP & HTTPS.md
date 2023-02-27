# HTTP & HTTPS

## HTTP (Hyper Text Transfer Protocol)

![image](https://user-images.githubusercontent.com/63834758/221482278-cab3ed7a-9f0c-49e5-9bc9-28143167a199.png)

  
- 서버와 클라이언트간에 데이터를 주고 받는 프로토콜  
- 서버에서 브라우저로 전송되는 정보가 암호화되지 않는 보안적 허점



## HTTPS (Hyper Text Transfer Protocol Secure)
  
- HTTP에 데이터 암호화가 추가된 프로토콜
- SSL(보안 소켓 계층)로 암호화된 연결 형성
- TLS(전송 계층 보안) 프로토콜로 보안 유지
    - 데이터 무결성 보장
    - 데이터 전송 중 수정 및 손상 방지
    - 사용자가 자신이 의도하는 웹사이트와 통신하고 있음을 입증하는 인증 기능 제공
- 참고 : [SSL/TLS](https://github.com/SeoYeonBae/CS_study/blob/main/Network/TLS%26SSL%20HandShake.md)


 
### HTTPS의 동작 과정

대칭키 암호화 & 비대칭키 암호화 모두 사용 -> 빠른 연산 속도 & 안정성

- 처음 연결을 성립하여 안전하게 세션키를 공유하는 과정 -> 비대칭키 사용 
- 이후 데이터 교환하는 과정에서 빠른 연산 속도를 위해 -> 대칭키(세션키) 사용
 
 
 
 

실제 HTTPS 연결 과정이 성립되는 흐름

1. 클라이언트(브라우저)가 서버로 최초 연결 시도
2. 서버는 공개키(엄밀히는 인증서)를 브라우저에게 넘겨줌
3. 브라우저 : 인증서의 유효성 검사 -> 세션키 발급
4. 브라우저 : 세션키 보관 + 추가로 서버의 공개키로 세션키를 암호화하여 서버로 전송함
5. 서버는 개인키로 암호화된 세션키를 복호화하여 세션키를 얻음
6. 클라이언트와 서버는 동일한 세션키를 공유하므로 데이터를 전달할 때 세션키로 암호화/복호화를 진행함

 ![image](https://user-images.githubusercontent.com/63834758/221483730-a07d795d-3859-4918-8140-4633632b293e.png)


<hr>


#### 참고자료

- [HTTP와 HTTPS의 개념 및 차이점](https://mangkyu.tistory.com/98)
- [인터넷 프로토콜 http와 https의 차이](https://post.naver.com/viewer/postView.nhn?volumeNo=16561296&memberNo=1834)
