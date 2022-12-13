# :pushpin: 인터럽트(Interrupt)

## :computer: 인터럽트란?

- CPU가 프로그램을 실행하고 있을 때, 입출력 하드웨어 등의 장치에 예외상황이 발생하여 처리가 필요할 경우에 CPU에게 알려 처리할 수 있도록 하는 것
- 인터럽트는 크게 하드웨어 인터럽트와 소프트웨어 인터럽트로 나뉨
- 필요한 이유는?
  - 상태를 **주기적으로 검사**하여 조건을 만족하면 처리를 하는 방식인 **폴링 방식**에 비해 문제 발생 시에만 처리를 하는 **인터럽트 방식**이 더 효율적이고 CPU에 부담이 덜 가기 때문에 필요
- 인터럽트 예시
  - 0으로 나누는 계산
  - **타이머 인터럽트**
  - 입출력 (I/O) 인터럽트

<br/>

---

<br/>

## :computer: 하드웨어 인터럽트 (외부 인터럽트)

- 하드웨어가 발생시키는 인터럽트
- 입출력 장치, 타이밍 장치, 전원 등의 외부적인 요인에 의해서 발행하는 인터럽트

      - 전원 이상 인터럽트
      - 기계 고장 인터럽트
      - 타이머 인터럽트 (선점형 스케쥴러에 필요)
      - 입출력 인터럽트

<br/>

---

<br/>

## :computer: 소프트웨어 인터럽트 (내부 인터럽트)

- 소프트웨어가 발생시키는 인터럽트
- 잘못된 명령이나 데이터를 사용할 때 발생하는 인터럽트

      - 0으로 나누는 계산
      - 오버플로우 또는 언더플로우가 발생한 경우
      - 프로그램에서 함수 등 명령어를 잘못 사용한 경우

<br/>

---

<br/>

## :computer: 주요 인터럽트

:heavy_check_mark: 타이머 인터럽트

- **선점형 스케쥴러**에 필요 (시분할)
  - 선점형 스케쥴러란 : 하나의 프로세스가 다른 프로세스 대신에 CPU를 차지할 수 있는 방법
- 10초마다 프로세스를 교체하는 시분할 선점형 스케쥴러일 경우
  1. 일정 간격으로 인터럽트를 계속해서 발생시킴
  2. 그것을 받은 운영체제는 해당 인터럽트를 누적시켜서 가지고 있음
  3. 인터럽트의 누적이 10초가 되는 순간 운영체제는 프로세스를 교체해야 하는 시기임을 알 수 있음

:heavy_check_mark: 시스템 콜이 발생시키는 인터럽트

<br/>

---

<br/>

## :computer: 인터럽트 과정

![image](https://user-images.githubusercontent.com/69101568/207267765-1eef7177-056c-49e6-b88e-cd4f59af450c.png)

![image](https://user-images.githubusercontent.com/69101568/207267603-83ddfb00-9249-45ce-866e-cac2413c8e82.png)

_process A 실행 중 디스크에서 어떤 데이터를 읽어오라는 명령을 받았다고 가정해보자!!!_

1. process A는 [System Call](<https://github.com/SeoYeonBae/CS_study/blob/main/OperatingSystem/%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EC%BD%9C(System%20Call).md>)을 통해 인터럽트를 발생시킴
2. CPU는 현재 진행 중인 기계어 코드를 완료
3. 현재까지 수행중이던 상태를 해당 process의 **PCB**에 저장
4. [PC(Program Counter)](<https://github.com/SeoYeonBae/CS_study/blob/main/ComputerArchitecture/%EC%A4%91%EC%95%99%EC%B2%98%EB%A6%AC%EC%9E%A5%EC%B9%98(CPU)%20%EC%9E%91%EB%8F%99%20%EC%9B%90%EB%A6%AC.md>)에 다음 실행할 명령의 주소 저장
5. **인터럽트 벡터**를 읽고 ISR 주소값을 얻어 **ISR**(interrupt Service Routine)으로 점프하여 루틴을 실행
6. 해당 코드 실행
7. 해당 일을 다 처리하면 저장했던 프로세스 상태 복구
8. ISR의 끝에 **IRET** 명령어에 의해 인터럽트 해제
9. IRET 명령어가 실행되면, 대피시킨 PC 값을 복원하여 이전 실행위치로 복원

<br/>

:heavy_check_mark: 인터럽트 용어 정리

- PCB
  - 수행중이던 메모리 주소, 레지스터 값, 하드웨어 상태 등을 저장하는 공간
  - 커널 데이터 영역에 존재
- ISR

  - 인터럽트 핸들러라고도 함
  - 실제 인터럽트를 처리하기 위한 루틴

- 인터럽트 벡터
  - ISR의 주소를 보관하는 공간
  - [인텔x86](https://github.com/SeoYeonBae/CS_study/blob/main/ComputerArchitecture/ARM%ED%94%84%EB%A1%9C%EC%84%B8%EC%84%9C.md)에서는 이를 IDT(Interrupt Descriptor Table)라고 함
- IRET
  - 이전 태스크로 다시 돌아가는 어셈블리 명령어
  - ISR의 마지막 명령어

<br/>

---

<br>

참고

- [OS기초 인터럽트 제대로 이해하기](https://velog.io/@adam2/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8)
- [운영체제 | 인터럽트는 무엇이고 왜 필요한가](https://velog.io/@hyun0310woo/7.-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)
- [OS Interrupt 인터럽트란?](https://doh-an.tistory.com/31)
- [운영체제 - 인터럽트](https://analysis-flood.tistory.com/135)
