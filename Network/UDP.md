
### 🛑 잠 깐 멈 춰 봐 (feat. IKON - ✈️)

![image](https://user-images.githubusercontent.com/63505110/220222738-577d21a1-413e-418e-b443-44114a6c5dbb.png)



#### 1️⃣ 전송계층(Transport layer, IOS 7계층)
  - 네트워크 계층과 세션 계층 사이에서 송수신되는 데이터를 안전하게 전달해주는 계층
  - End Point 간 신뢰성있는 데이터 전송을 담당하는 계층
    - 신뢰성 : 데이터의 순차적, 안정적인 전달
    - 전송 : 포트 번호에 해당하는 프로세스에 데이터 전송

## TCP (Transmission Control Protocol)
- 연결형 
  - 3-way handshake 과정을 통해 연결 설정
  - 4-way handshake 과정을 통해 연결 해제
- **신뢰성** 보장
  - 순서대로 에러없이 교환
- 데이터 흐름 제어(수신자 버퍼 오버플로우 방지) 및 혼잡 제어(패킷 수가 과도하게 증가하는 현상 방지)


단점
- 데이터로 보내기 전에 반드시 연결이 형성되어야 함
- 1:1 통신만 가능
- 신뢰성 보장하는 대신 속도 느림
                   

## UDP (User Datagram Protocol)
- 비 연결형 (Connectionless)
  - 데이터그램 방식 제공
  - Client는 패킷을 확인하지 않고 무조건 송신
  - Server는 소켓 무조건 열어두고 있음
  - 별도의 연결 설정이나 해제 과정이 존재 X
  - 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다.
- 오류 검출
  - UDP 헤더의 CheckSum 필드를 통해 최소한의 오류만을 검출한다.
- 빠른 속도


단점
- 데이터 신뢰성 없음
- TCP와 다르게 데이터를 쪼개주지 않아 애플리케이션 단에서 패킷을 직접 쪼개 관리해주어야 함
             
  
## ⚠️ 정 리
### 공통점
- 포트 번호를 이용하여 주소 지정
- 데이터 오류 검사를 위한 CheckSum 존재
- 암호화 제공하지 않음

          
### 차이점
||TCP|UDP|
|---|----|---|
|연결성|연결 지향형|비연결 지향형|
|패킷 교환 형식|Connection Oriented Service : 가상 회선 방식|Connectionless Oriented Serive : 데이터그램 방식|
|전송 순서|전송 순서 보장|전송 순서 바뀔 수 있음|
|수신 여부 확인|수신 여부 확인|수신 여부 확인하지 않음|
|통신 방식|1:1 통신만 가능|1:1 / 1:N / N:N 통신 모두 가능|
|신뢰성|높음|낮음|
|속도|느림|빠름|

-----------
###### 참고

- https://velog.io/@given53/CS-Network-TCP-UDP
- https://velog.io/@litien/%EB%A9%B4%EC%A0%91%EC%8A%A4%ED%84%B0%EB%94%94-TCP-UDP
