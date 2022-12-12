# :pushpin: 시스템 콜(System Call)란?

:heavy_check_mark: 운영체제 구동

    운영체제는 커널 모드(Kernel Mode)와 사용자 모드(User Mode)로 나뉘어 구동된다.
    운영체제에서 프로그램이 구동되는데 있어 파일을 읽어오거나, 쓰거나, 혹은 화면에 메시지 출력하는 등 많은 부분이 커널 모드를 사용한다.
    운영체제는 다양한 서비스들을 수행하기 위해 하드웨어를 직접적으로 관리하지만
    이에 반해 응용 프로그램은 운영체제가 제공하는 인터페이스(System Call)를 통해서만 자원을 사용할 수 있다.

---


## :computer: 시스템 콜(System Call)의 정의
- 커널 영역의 기능을 사용자 모드가 사용 가능하게, 즉 프로세스가 하드웨어에 직접 접근해서 필요한 기능을 사용할 수 있게 해주는 것
- 시스템 호출(system call)은 운영 체제의 커널이 제공하는 서비스에 대해, 응용 프로그램의 요청에 따라 커널에 접근하기 위한 인터페이스
- 보통 C나 C++과 같은 고급 언어로 작성된 프로그램들은 직접 시스템 호출을 사용할 수 없기 때문에 고급 API를 통해 시스템 호출에 접근하게 하는 방법

  ![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJXwNG%2Fbtqw787Kgfe%2FvmrkitiEEjDI8G9w2mFzUk%2Fimg.png)

 


## :computer: 시스템 콜의 유형

:heavy_check_mark: 프로세스 제어(Process Control)

- 끝내기(end), 중지(abort)
- 적재(load), 실행(execute)
- 프로세스 생성(create process)
- 프로세스 속성 획득과 설정(get process attribute and set process attribute)
- 시간 대기(wait time)
- 사건 대기(wait event)
- 사건을 알림(signal event)
- 메모리 할당 및 해제 : malloc, free

:heavy_check_mark: 파일 조작(File Manipulation)
- 파일 생성(create file), 파일 삭제(delete file)
- 열기(open), 닫기(close)
- 읽기(read), 쓰기(write), 위치 변경(reposition)
- 파일 속성 획득 및 설정(get file attribute and set file attribute)


:heavy_check_mark: 장치 관리(Devide Management)
- 장치를 요구(request devices), 장치를 방출release device)
- 읽기, 쓰기, 위치 변경
- 장치 속성 획득, 장치 속성 설정
- 장치의 논리적 부착(attach) 또는 분리(detach)


:heavy_check_mark: 정보 유지(Information Maintenance)
- 시간과 날짜의 설정과 획득(time)
- 시스템 데이터의 설정과 획득(date)
- 프로세스 파일, 장치 속성의 획득 및 설정

:heavy_check_mark: 통신(Communication)
- 통신 연결의 생성, 제거
- 메시지의 송신, 수신
- 상태 정보 전달
- 원격 장치의 부착 및 분리

  :heavy_check_mark: 일반적인 통신 모델에는 *메시지 전달*과 *공유 메모리*  두가지가 있다.
  - 메시지 전달 모델에서는 두 프로세스의 통신에 정보 교환을 위한 메시지를 주고 받는다.
  - 공유 메모리 모델에서는 다르프로세스가 소유한 메모리에 접근을 위해 특정 시스템 콜을 호출한다.
    - 일반적으로 운영체제는 서로 다른 프로세스간의 메모리 접근을 차단한다.
    - 공유 메모리 기법을 사용하기 위해서는 통신하려는 프로세스들이 이러한 차단을 풀어주는데 동의해야 한다.


:heavy_check_mark: 보호(Protection)
- chmod()
- umask()
- chown()

---

<br>

참고

- [운영체제 04 : 시스템 콜 (시스템 호출, System Call)](https://luckyyowu.tistory.com/133)
