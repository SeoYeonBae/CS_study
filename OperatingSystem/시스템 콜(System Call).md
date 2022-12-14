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
- 시스템 콜은 여러 종류의 기능으로 나뉘어져 있는데 각 시스템 콜에는 번호가 할당되고 시스템 콜 인터페이스는 이러한 번호에 따라 인덱스되는 테이블 유지
    - Ex. open() 시스템 콜을 호출
    ![sc](https://user-images.githubusercontent.com/63505110/207511504-88066e36-b978-4692-b73a-70f7020f580a.GIF)

  ![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJXwNG%2Fbtqw787Kgfe%2FvmrkitiEEjDI8G9w2mFzUk%2Fimg.png)           
    - 사용자 모드에 있는 응용 프로그램이 커널의 기능을 할 수 있도록 한다.
    - 시스템 호출을 하면 사용자 모드에서 커널 모드로 바뀐다.
    - 커널에서 시스템 호출을 처리하면 커널 모드에서 사용자 모드로 돌아가 작업을 계속한다.


- 우리가 일반적으로 사용하는 프로그램은 '응용프로그램'
- 유저레벨의 프로그램은 유저레벨의 함수들 만으로는 많은 기능을 구현하기 힘들기 때문에, 커널(kernel)의 도움을 반드시 받아야 함
- 이러한 작업은 응용프로그램으로 대표되는 유저 프로세스(User Process)에서 유저모드로 수행할 수 없음
- 반드시 kernel에 관련된 것은 커널모드로 전환한 후에야, 해당 작업을 수행할 권한이 생기는데 커널 모드를 통한 이러한 작업은 반드시 **시스템 콜**을 통해 수행하도록 설계되어 있음

## ❓ 왜 이렇게 사용하는걸까?
-  해커가 피해를 입히기 위해 악의적으로 시스템 콜을 사용하는 경우나 초보 사용자가 하드웨어 명령어를 잘 몰라서 아무렇게 함수를 호출했을 경우에 시스템 전체를 망가뜨릴 수도 있기 때문
- 그렇기에 이러한 명령어들은 특별하게 커널 모드에서만 실행할 수 있게 설계

## :computer: 시스템 콜(System Call) 매개변수 전달

- 필요한 기능이나 시스템 환경에 따라 시스템 콜이 발생할 때 좀 더 많은 정보가 필요할 수 있는데 그러한 정보가 담긴 매개변수를 운영체제에 전달하기 위해 대략 3가지 방법 존재
    1. 매개변수를 CPU 레지스터 내에 전달
        - 이 경우 매개변수의 개수가 CPU 내의 총 레지스터 개수보다 많을 수 있음
    2. 위와 같은 경우 매개변수를 메모리에 저장하고 메모리의 주소를 레지스터에 전달
    3. 매개변수는 프로그램에 의해 스택(Stack)으로 전달(push) 될 수 있음
        - 2,3번 방법의 경우 전달되는 매개변수의 개수나 길이에 제한이 없기에 몇몇 운영체제에서 선호하는 방식



 


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

- https://luckyyowu.tistory.com/133
- https://fjvbn2003.tistory.com/306
