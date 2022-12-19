# 📌 CPU 스케줄링

> 프로세스는 CPU에 할당을 받아 작업을 수행 그렇다면 여러 프로세스 중 누가 CPU의 할당을 받을 것인가?


## ⏰ 1. 프로세스의 단계와 CPU 스케줄링

### ❗프로세스의 상태전이

 - 프로세스가 생성되고 난 뒤 거치게 되는 상태
 - 프로세스의 상태 전이는 아래와 같이 New(생성), Ready(준비), Running(실행), Blocked(대기), Terminated(종료)로 나뉨
      
 ![image](https://user-images.githubusercontent.com/101535851/208393006-eaebf2fa-d197-4323-84e3-49c843d2ba53.png)

  - 생성(New)
         
     - 제일 첫번째로 New에서 Ready로 전이되는 과정
     - 프로세스가 생성되고 나서 생성된 프로세스는 준비(Ready) 상태에 머뭄
     - 준비 상태는 CPU를 점유하고 있는 상태가 아니라, CPU를 점유하길 희망하는 상태
     - 준비 상태에서 실행 상태로 넘어가려면 작업 스케줄러가 선택해 주어야만 함 -> CPU 스케줄링

  - 🌟 디스패치(Dispatch)
      
    - 디스패치란 준비 상태에서 실행 상태로 전이되는 과정
    - 작업 스케줄러가 해당 프로세스를 선택하여 실행되어지는 것
    - 이때 실행된 프로세스가 CPU를 점유
     
  - 인터럽트(Interrupt)
      
    - 인터럽트 신호 -> 실행중이던 프로세스는 준비 상태로 전이 -> 우선순위(Priority)가 높은 프로세스를 실행 상태로 전이
    - 프로세스는 각각 우선순위를 부여받고, 우선순위에 따라 프로세스가 준비 상태로 전이되거나, 실행 상태로 전이됨

  - 입출력 혹은 이벤트 대기(I/O or event wait)
      
    - CPU를 점유하고 있는 프로세스가 입출력 처리를 해야만 하는 상황
     - 실행되고 있는 프로세스는 실행 상태에서 대기/보류 상태로 바뀌고 대기 상태로 바뀐 프로세스는 입출력 처리가 모두 끝날때까지 대기 상태로 머뭄
     - 실행 상태이던 프로세스가 대기 상태로 전이됨과 함께 준비 상태이던 또다른 프로세스가 실행 상태로 전이
     - 대기 상태인 프로세스는 우선순위가 부여되지 않으며 스케줄러에 의해 선택될 수 없음

   - 입출력 혹은 이벤트 완료(I/O or event completion)
      
     - 입출력 처리가 끝난 프로세스는 대기 상태에서 준비 상태로 전이되어 스케줄러에게 선택될 수 있게 됨
     - 추가로 프로세스를 종료(Terminate)시킬 때에도 Blocked 상태를 거칠 수 있다는 사실을 기억해 두시길 바랍니다.

## ⏰ 2. 비선점 스케줄링과 선점 스케줄링

### 1️⃣ 비선점

  - 프로세스 종료 or I/O등의 이벤트가 있을 때까지 실행 보장
  - 장점
     - 모든 프로세스들에게 공정하다.
     - 응답 시간을 예측할 수 있다.
   - 단점
     - 짧은 작업을 수행하는 프로세스라도 긴 작업이 종료될 때까지 기다려야 할 수 있다.

### 2️⃣ 선점
    
   - OS가 CPU의 사용권을 선점할 수 있는 경우 강제로 회수
   - 장점
     - 높은 우선 순위를 가진 프로세스를 빠르게 처리하려는 시스템에 유용
     - 빠른 응답 시간을 요구하는 시분할 시스템에 유용
   - 단점
     -  높은 우선 순위를 가진 프로세스만 들어오는 경우 overhead 발생


## ⏰ 3. 비선점 스케줄링의 종류

### 1️⃣ FCFS (First Come First Served) : 선입 선처리 알고리즘
     
  ![image](https://user-images.githubusercontent.com/101535851/208408126-07b452b8-bc5a-4e31-92d7-b82131e1977f.png)
     
  - 큐에 도착한 순서(CPU를 요청한 순서)대로 CPU 할당
  - 장점
    - 우선 순위가 낮은 프로세스가 무작정 기다리는 상황인 Starvation(기아 상태) 이슈가 발생하지 않음
  - 단점
    - 실행 시간이 짧은 게 뒤로 가면 평균 대기 시간이 길어짐
    - 실행 시간이 긴 프로세스가 먼저 도달할 경우 효율성이 낮아짐

### 2️⃣ SJF (Shortest Job First) : 최단 작업 우선 스캐줄링
  - FCFS 알고리즘을 보완하기 위해 만들어짐
  - 수행 시간이 가장 짧다고 판단되는 작업을 먼저 수행
  - 장점
    - FCFS보다 평균 대기 시간 감소, 짧은 작업에 유리
  - 단점
    - 점유 불평등 
    - 사용 시간이 긴 프로세스는 영원히 CPU를 할당받지 못할 수 있음 -> Starvation 발생

### 3️⃣ HRN (Hightest Response-ratio Next)
  - 우선순위를 계산하여 점유 불평등을 보완한 방법(SJF의 단점 보완)
  - 우선순위 = (대기시간 + 실행시간) / (실행시간)


## ⏰ 4. 선점 스케줄링의 종류

### 1️⃣ Priority Scheduling : 우선순위 스케줄링
   
   - 정적 / 동적으로 우선순위를 부여해 우선순위가 높은 순서대로 처리
   - 선점 / 비선점 모두 접목 가능
   - 단점
     - Starvation or Indefinite Blocking 발생할 수 있음
     - Starvation: 높은 우선순위의 프로세스들이 꾸준히 들어와서 낮은 우선순위의 프로세스들이 CPU를 얻지 못함
     - Indefinite: 실행 준비는 되어 있으나 CPU를 사용하지 못하는 프로세스는 CPU를 기다리면서 봉쇄 된 것으로 간주
   - Aging 방법으로 Starvation 문제 해결 가능
     - Aging: 시스템에서 오랫동안 대기하는 프로세스들의 우선순위를 점진적으로 증가

### 2️⃣ Round Robin Scheduling : 라운드 로빈 스케줄링
 
   ![image](https://user-images.githubusercontent.com/101535851/208408916-314fb641-f2a1-43ec-ad66-9b57107d8422.png)
    
   - 각 프로세스가 주로 10 ~ 100ms의 동일한 크기의 할당 시간(Time quantum)을 갖음
   - 할당 시간이 끝나면 프로세스는 자동으로 선점(Preempted)당하고, Ready queue의 제일 뒤에 가서 다시 줄을 섬
    
### 3️⃣ Multilevel-Queue : 다단계 큐

   ![image](https://user-images.githubusercontent.com/101535851/208409816-a0595e59-a95d-4f0b-afb7-ecb5cd7f053a.png)

   - Ready Queue를 여러 개로 분할한 것
   - 우선순위가 낮은 큐들이 실행하지 못하는 것을 방지하고자 각 큐마다 다른 Time quantum을 설정
   - 우선순위가 높은 큐는 작은 Time quantum, 낮은 큐는 높은 Time quantum

### 4️⃣ Multilevel-Feedback-Queue : 다단계 피드백 큐

   ![image](https://user-images.githubusercontent.com/101535851/208410523-aa345a05-bc18-4d89-ace0-373b330884c2.png)
      
   - 다단계 큐에서 자신에게 할당된 Time Quantum을 다 사용한 프로세스는 밑으로 내려가고 Time Quantum을 다 채우지 못한 프로세스는 원래 큐 위치 그대로 둠
   - 짧은 작업에 유리하며 입출력 위주의 작업에 우선권을 줌
   - 처리 시간이 짧은 프로세스를 먼저 처리하기 때문에 총처리 시간의 평균 시간을 줄임

## ✔️ 5. 스케줄링 알고리즘 평가(비교) 기준

> 여러 CPU 스케줄링 알고리즘들 중 하나를 선택하기 위한 평가 기준

- CPU 이용률(Utilization): CPU를 쉬지 않고 계속 돌려야 한다
- 처리량(Throughput): 단위 시간당 완료된 프로세스의 개수로 나타낼 수 있다
- 총처리 시간(Turnaround Time): 수행을 요청한 후 작업이 끝날 때까지 걸린 시간
- 대기 시간(Waiting Time): 수행을 요청한 후 작업이 시작될 때까지 걸린 시간
- 응답 시간(Response Time): 요청 후 첫 번째 응답이 나올 때까지의 시간

> <strong>CPU Utilitzation, Throughput은 늘리고, Time 지표들은 감소하는 것이 스케줄링 목표가 된다</strong>


## ✔️ 6. System에 따른 스케줄링의 목표

> 사용하는 시스템에 따라 스케줄링의 세부 목표가 달라짐

### 1️⃣ Batch System
  
  - Batch System: 한 번에 하나의 프로그램만 수행하는 시스템
  - 총처리 시간(Turnaround Time)이나 응답 시간(Response Time)과 같은 시간이 중요한 게 아니라 처리량(Throughput)이 중요
  
### 2️⃣ Interactive System

  - 사용자가 컴퓨터 앞에서 대화형으로 동작하는 시스템
  - 가장 중요한 것은 응답 시간(Response Time)과, 대기 시간(Waiting Time)
  - 하나의 작업이 끝날 때까지 오랫동안 기다리면 안 된다는 뜻

### 3️⃣ Real-time System

  - 주어진 input에 output만 계산하는 것이 전부가 아닌 시간 제약 조건이 걸려 있는 시스템
  - 따라서 기한을 맞추는 것이 가장 중요

---

##### 참고
- [시스템에 따른 스케줄링의 목표](https://jhnyang.tistory.com/29?category=815411)
- [프로세스 스케줄링](https://blog.hexabrain.net/256)
- [CPU Scheduling](https://gyoogle.dev/blog/computer-science/operating-system/CPU%20Scheduling.html)
- [CPU 스케줄링 (CPU Scheduling)](https://runa-nam.tistory.com/88)
- [[운영체제] CPU 스케줄링](https://steady-coding.tistory.com/509)
- [[운영체제(OS)] 5. 프로세스 스케줄링(Process Scheduling) - 스케줄링 방법 예시 자세함](https://rebro.kr/175)
