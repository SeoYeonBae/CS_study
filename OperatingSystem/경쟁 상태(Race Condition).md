# :pushpin: 경쟁상태(Race Condition)

## :computer: 경쟁상태란?

- 여러 개의 Thread나 Process가 하나의 공유 자원을 동시에 접근하는 상황
- 데이터 불일치를 발생시킬 수 있음 (data inconsistency)

---

## :computer: OS에서의 경쟁상태

- 커널 코드 수행 중에 인터럽트가 발생한 경우

  ![image](https://user-images.githubusercontent.com/69101568/208452690-deeabd23-0458-48cf-9654-0a7357289bc7.png)

- Process가 System Call을 요청하여 커널 모드로 수행 중에 Context Switch가 발생한 경우

  ![image](https://user-images.githubusercontent.com/69101568/208452935-99ff4116-69e8-4532-92a8-a3f4c4d5ce7d.png)

- Multi-Processor환경에서 Shared-Memory로 커널 접근 시

  ![image](https://user-images.githubusercontent.com/69101568/208448557-140943b8-2d1b-46ca-9fa2-80b4c0196438.png)

---

## :computer: 임계영역(Critical Section)이란?

- 경쟁상태가 발생할 수 있는 코드 조각
- Thread 또는 Process가 공유하고 있는 변수가 있는 코드 조각

  ![image](https://user-images.githubusercontent.com/69101568/208454735-fa2d749a-2bb9-45bb-9600-09e13a0888b8.png)

  _Multi-Processor 환경에서 임계영역_

:heavy_check_mark: 임계영역 문제 (Critical Section Problem)

- 임계영역에서 경쟁상태가 발생한 것을 임계영역 문제라고 한다!!!
- 즉, 임계영역 문제를 해결한다는 것은 경쟁상태를 해결한다는 것

---

## :computer: 경쟁상태 해결조건 3가지

_3가지 조건을 만족한다면 경쟁상태를 해결할 수 있다!_

1. Mutual Exclusion (상호 배제)
   - 하나의 자원에는 하나의 프로세스만 접근할 수 있어야 함
2. Progress (진행)
   - 아무도 임계영역에 있지 않다면, 다음에 어떤 프로세스 혹은 쓰레드가 임계영역에 진입해야 하는지 유한한 시간에 결정되어야 함
   - 즉, 임계영역에 있는 프로세스 외에는 다른 프로세스가 임계영역에 진입하는 것을 방해할 수 없음
3. Bounded Waiting (한정 대기)
   - 임계영역에 진입하기 위해 무한정으로 기다리는 현상(Starvation)이 발생해서는 안됨

---

## :computer: Peterson's Solution

_경쟁상태가 발생하지 않게 하는 방법 -> Thread의 **순차적 실행** (동기화)_

:heavy_check_mark: Peterson's Solution

![image](https://user-images.githubusercontent.com/69101568/208463863-31d59605-90c6-4d75-8e40-5a52c0587dbb.png)

- 동기화 방법 중 하나
- two processes synchronization을 위한 해결책
- **유저모드의 동기화**
  - 커널의 힘을 빌리지 않는 동기화 기법
- 두 개의 프로세스는 두 개의 변수를 공유함
  - int turn
    - 누가 임계영역에 들어갈 차례인지
  - boolean flag[2]
    - 임계영역에 들어갈 준비가 되있는지 아닌지
    - flag[i] = true이면 Pi가 준비되었음을 의미
- 단점
  - **소프트웨어적 방법**이라 도중에 context switch가 발생할 수 있다
  - 프로세스가 2개인 경우에만 적용 가능
  - 임계영역에 들어가기 위해 기다리고 있는 프로세스는 무한 루프를 돌며 entry section에 머무르는데 이때 CPU를 계속 써서 낭비함 (Busy Waiting)

---

<br>

참고

- [5주차.프로세스 동기화(1)-race condition](https://ws-pace.tistory.com/25)
- [운영체제 | 5.Race Conditions(1)](https://howisitgo1ng.tistory.com/entry/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-5-Race-Conditions)
- [OS Race Condition 경쟁상태란?](https://zangzangs.tistory.com/115)
- [운영체제 - 경쟁상태와 동기화의 필요성, 임계 구역](https://charles098.tistory.com/88)
- [운영체제 - 동기화 방법1 Peterson's Solution](https://charles098.tistory.com/91)
- [운영체제 - 경쟁상태 (Race Condition)](https://velog.io/@klloo/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B2%BD%EC%9F%81-%EC%83%81%ED%83%9C-Race-Condition)
