# :pushpin: OSI 7계층

## :computer: OSI 7계층이란???

_OSI 7 계층은 네트워크에서 통신이 일어나는 과정을 7단계로 나눈 것을 말하며, 국제 표준화 기구에서 네트워크 간의 호환을 위해 OSI 7 계층이라는 표준 네트워크 모델을 만들었다_

:heavy_check_mark:  OSI 7단계로 정의한 이유

- 통신이 일어나는 과정을 단계별로 파악하기 위함
- 통신 과정 중에 특정한 곳에 이상이 생길 경우에 **다른 단계의 장비 및 소프트웨어 등을 건드리지 않고 통신 장애를 일으킨 단계에서** 해결할 수 있기 때문

---

## :computer: OSI 7 계층 구조

![image](https://user-images.githubusercontent.com/69101568/216804019-bea3962b-3e6b-49e6-baef-a81ee9fe6004.png)

_OSI 7 계층과 계층별 해당하는 프로토콜 이미지_

---

## :one: 계층 : 물리 계층 (Physical Layer)
- 실제 장치를 연결하기 위한 전기적 및 물리적 세부 사항을 정의한 계층
- 인터넷 케이블, 라우터 스위치 등의 **전기적 신호**가 물리적인 장치에 의해 통신하는 계층
- 전송 또는 받는 데이터가 무엇인지, 어떤 에러가 있는진는 신경 쓰지 않음
- ex) 통신 케이블, 리피터, 허브 등

---

## :two: 계층 : 데이터 링크 계층 (Data Link Layer)
- 장치 간 신호를 전달하는 물리계층을 이용하여 네트워크 상의 주변 장치들 간의 데이터를 전송하는 역할
- 물리계층을 통해 송수신되는 정보의 오류와 흐름을 관리하여 **안전한 정보의 전달**을 수행하도록 도움
- **맥 주소**를 가지고 통신
- 두 장치간의 **신뢰성 있는 전송**을 보장
- 데이터 링크 계층에서 전송되는 단위를 프레임이라 하고, 대표적인 장비는 브리지, 스위치가 있음
  
---

## :three: 계층 : 네트워크 계층 (Network Layer)
- 여러 개의 노드를 거칠 때마다 경로를 찾아주는 역할
- 경로를 선택하고 주소를 정하고 경로에 따라 패킷을 전달해주는 것이 이 계층의 주 역할
- 대표적인 장비는 라우터가 있음
- 라우팅, 흐름 제어, 세그멘테이션, 오류 제어, 인터네트워킹 등을 수행
  
---

## :four: 계층 : 전송 계층 (Transport Layer)
- 통신을 활성화하기 위한 계층
- 보통 TCP 프로토콜 이용
- 데이터가 왔다면 해당 데이터를 하나로 통합하여 5계층으로 전달
- **양 끝단의 사용자가 신뢰성 있는 데이터를 주고받게 하여** 상위 계층이 데이터 전달의 유효성이나 효율성을 신경 쓰지 않게 해주는 계층

---

## :five: 계층 : 세션 계층 (Session Layer)
- 양 끝단의 응용 프로세스가 통신을 관리하는 방법을 제공하는 계층
- 이 계층의 프로토콜은 통신 연결이 손실되는 경우 연결 복구 시도가 가능하며 연결 시도중 장시간 연결이 되지 않았다면 세션 계층의 프로토콜이 연결을 닫고 다시 연결을 시도
- **동기화**
  
      - 전이중 통신(Full Duplex)
        - 두 대의 단말기가 데이터를 송수신하기 위해 동시에 각각 독립된 회선을 사용하는 통신방식
        - ex) 전화망, 고속 데이터 통신
      - 반이중 통신(Half Duplex)
        - 한쪽이 송신하는 동안 다른 쪽에서 수신하는 통신방식
        - 마스터 슬레이브 방식의 센서 네트워크가 대표적

---

## :six: 계층 : 표현 계층 (Presentation Layer)
- 코드 간 변역을 담당하는 계층
- 사용자 시스템에서 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어주고 MIME 인코딩이나 암호화 등의 동작이 이루어짐
- 예를 들면, EBCDIC로 인코딩된 문서 파일을 ASCII로 인코딩된 파일로 바꿔주는 것

---

## :seven: 계층 : 응용 프로그램 계층 (Application Layer)
- 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행하는 계층
- 최상위 계층으로 사용자에게 직접적으로 보이는 부분

---

<br>

참고

- [[네트워크]  OSI 7Layer / 7계층 개념 및 역할,구조까지 한번에 알아보기](https://onecoin-life.com/19)
- [OSI 7 계층이란?, OSI 7 계층을 나눈 이유](https://shlee0882.tistory.com/110)