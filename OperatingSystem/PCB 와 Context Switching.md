# 📌PCB 와 Context Switching

#### ✔️프로세스 관리

- 구동 중인 프로세스가 여러 개 일때, CPU 스케줄링으로 프로세스를 관리하는 것
- 이 때 CPU는 프로세스들의 본연의 특징을 갖고 있는 **Process Metadata**라는 정보를 활용

<hr>

### 💻Process Metadata

| 구성 정보                       | 설명                                                                                                                                                                           |
| :------------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Process ID**                      | 프로세스 고유 식별 번호                                                                                                                                                        |
| **Process State(프로세스 상태)**    | 프로세스의 현재 상태(준비, 실행, 대기 상태)를 기억                                                                                                                             |
| **Process Priority(스케줄링 정보)** | 프로세스 우선순위 등과 같은 스케줄링 관련 정보를 기억                                                                                                                          |
| **CPU Registers**                   | 프로세스의 레지스터 상태를 저장하는 공간 등. CPU 내 범용 레지스터(AX, BX, CX, DX), 데이터 레지스터(SP, BP, SI, DI), 세그먼트 레지스터(CS, DS, ES, SS) 등이 갖고 있는 값을 기억 |
| **Owner(계정 정보)**                | CPU 사용시간의 정보(Quantum), 각종 스케줄러에 필요한 정보를 기억                                                                                                               |
| **기억장치 관리 정보**              | 프로그램이 적재될 기억 장치의 상한치, 하한치, 페이지 테이블 등의 정보를 기억                                                                                                   |
| **입출력 정보**                     | 프로세스 수행 시 필요한 주변 장치, 파일들의 정보를 기억                                                                                                                        |
| **프로그램 카운터(계수기)**         | 다음에 실행되는 명령어의 주소를 기억                                                                                                                                           |

- 이러한 정보들이 담긴 Metadata는 프로세스가 생성되면 **PCB(Process Control Block)**이라는 곳에 저장된다.
- CPU의 프로세스 교체작업 진행 도중, 프로세스의 정보를 잃지 않기 위해 PC가 필요한 것이다.
<br>
<hr>


### 💻PCB(Process Control Block)

- 프로세스 Metadata들을 저장해 놓는 곳
- 하나의 PCB 안에는 하나의 프로세스 정보가 담겨있다.

![image](https://user-images.githubusercontent.com/63834758/207347092-5e36a899-989f-4c83-85a5-f3fe83516434.png)

#### ✔️PCB 관리 방식

- Linked List 방식
- PCB List Head에 PDB들이 생성될 때마다 붙게 된다.
- 즉 주솟값으로 연결된 Linked List 형태로, 삽입 및 삭제에 용이
- **프로세스가 생성되면 해당 PCB가 생성되고, 프로세스 완료시 제거된다.**

<br>
<hr>


### 💻Context Switching

#### ✔️정의

- CPU가 이전의 프로세스 상태를 PCB에 보관하고, 새로운 프로세스의 정보(Context)를 PCB에서 읽어서 레지스터에 적재하는 과정
- 발생 시기 : 인터럽트 발생, 현재 프로세스의 선점 허용 기간을 모두 소모한 상황, 입출력을 위해 대기하는 경우 등


<br>

#### ✔️수행 과정

1. Task의 대부분의 정보는 Register에 저장되고 PCB(Process Control Block)로 관리되고 있는 상태

2. 프로세스 교체상황 발생 시 현재 실행 중인 Task의 PCB 정보를 저장한다.

3. 다음 실행할 Task의 PCB 정보를 읽어 Register에 적재하고 CPU가 이전에 진행했던 과정을 연속적으로 수행할 수 있게 된다.


<br>

#### ✔️Context Switching Overhead
Thread 및 Process 개수 증가로 Context Switching 발생이 잦아지면, **프로세스의 실행을 위한 부가적인 활동(Overhead)**도 잦아져 성능이 악화될 수 있다.

<br>

#### ✔️Context Swiching과 시간 할당량
- 시간 할당량 감소 : Context Switching, 인터럽트 횟수, Overhead 증가 / **여러 개의 프로세스가 동시에 수행되는 느낌을 가짐.**

- 시간 할당량 증가 : Context Switching, 인터 럽트 횟수, Overhead가 감소 / **여러 개의 프로세스가 동시에 수행되는 느낌을 갖지 못함.**


<br>
<hr>

#### 참고자료

[PCB 와 Context Switching 알아보기](https://velog.io/@haero_kim/PCB-%EC%99%80-Context-Switching-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)
[PCB 와 Context Switching](https://velog.io/@heetaeheo/PCB-%EC%99%80-Context-Switching)
