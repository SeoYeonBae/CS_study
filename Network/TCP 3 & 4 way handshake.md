# 📌 TCP 3 & 4 way handshake


### TCP : _연결 지향형 프로토콜_ 
장치들 사이에 논리적인 접속 성립을 위해
신뢰성을 보장하는 연결형 서비스

- 전송되는 데이터의 신뢰성 보장 (흐름 제어, 혼잡 제어, 오류 제어)
- 가상 회선을 만들어 신뢰성을 보장
- 파일전송에 주로 사용
 
 
## 🌐 TCP 3 way handshake : _3번의 연결 확인 방식_

TCP 통신을 이용한 데이터 전송을 위해  
**네트워크 연결을 설정(Connection Establish)** 하는 과정
 
 
👸A →→ 🤴B : 내 말 들려?  
👸A ←← 🤴B : 잘 들려. 내 말은 들려?  
👸A →→ 🤴B : 잘 들려!  


![image](https://user-images.githubusercontent.com/63834758/218760424-e670a103-474e-4bc8-97dd-f92ae604857e.png)

 

 

### SYN (synchronize sequence numbers)
연결 확인을 위해 보내는 무작위의 숫자값 (내 말 잘 들려?)
  
### ACK (acknowledgements)
Client 혹은 Server로부터 받은 SYN에 1을 더해 SYN을 잘 받았다는 ACK (잘 들려)
 
### ISN (Initial sequence numbers)
Client와 Server가 각각 처음으로 생성한 SYN
 
 
 
## 🌐 TCP의 3-way Handshaking 과정
[STEP 1]  

- A클라이언트 : B서버에 접속을 요청하는 SYN 패킷을 보낸다.  
- SYN 을 보내고 SYN/ACK 응답을 기다리는 SYN_SENT 상태

 

[STEP 2] 

- B서버 : SYN요청을 받고 A클라이언트에게 
         요청을 수락한다는 ACK 와 SYN flag 가 설정된 패킷을 발송하고 
         A가 다시 ACK으로 응답하기를 기다린다.  
- B서버 : SYN_RECEIVED 상태

 

[STEP 3]  

- A클라이언트 : B서버에게 ACK을 보내고 이후로부터는 연결이 이루어지고 데이터가 오가게 된다. 
- B서버 : ESTABLISHED 상태  

 

 
 <hr>
   
   
  
  
## 🌐 TCP 4 way handshake : _4번의 확인 과정_

3 way handshake와 반대로  
**네트워크 연결을 해제(Connection Establish)** 하는 과정
 
 
![image](https://user-images.githubusercontent.com/63834758/218761735-b423ba60-1823-4227-9351-30ee29ef23fd.png)

 

 
👸A →→ 🤴B : 나는 다 보냈어. 이제 끊자!  

👸A ←← 🤴B : 알겠어! 잠시만~  
👸A ←← 🤴B : 나도 끊을게! 

👸A →→ 🤴B : 알겠어!


### 🌐 TCP의 4-way Handshaking 과정
  
[STEP 1]  
클라이언트 : 연결을 종료하겠다는 FIN플래그를 전송



[STEP 2]   
- 서버 : 일단 확인메시지를 보내고 자신의 통신이 끝날때까지 기다린다.
- TIME_WAIT 상태

 

[STEP 3]  
서버 : 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN플래그를 전송

 

[STEP 4]  
클라이언트 : 확인했다는 메시지를 전송

<hr>  


### 참고자료
- [[네트워크] TCP 3-way & 4-way handshake란?](https://seongonion.tistory.com/74)
- [TCP 3 Way-Handshake & 4 Way-Handshake](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake)
- [[Network] TCP 3-way handshaking과 4-way handshaking](https://gmlwjd9405.github.io/2018/09/19/tcp-connection.html)
