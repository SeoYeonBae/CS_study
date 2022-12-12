# :pushpin: IPC(Inter Process Communication)

:heavy_check_mark: 프로세스 간의 통신
- 프로세스는 독립적으로 실행 (반면, 스레드는 프로세스 안에서 자원을 공유)
- 독립적 구조를 가진 **프로세스 간의 통신**을 가능하게 하는 것이 **IPC** 통신
- 커널이 제공하는 IPC 설비를 이용해 프로세스 간 통신을 함

---
## :computer: IPC의 두가지 모델
:heavy_check_mark: Message Passing
- 커널을 거쳐서 메세지를 전달하는 방식
- Kernel을 활용하기에 쉽게 구현할 수 있고 같은 파일을 전달하는 데 있어서 conflict가 발생하지 않음
- 직접 전달에 비해 속도가 느림
- user level과 kernel level을 넘나들기 때문에 매번 system call이 호출되고 이로 인한 overhead
- 전달할 내용이 도착하기 전에 또 보내라는 신호를 보낸다면 -> Blocking(원하는 작업을 수행할 때까지 나머지 차단) / Non-blocking(막지 않고 그대로 반응)

:heavy_check_mark: Shared Memory
- 프로세스들이 공유하는 메모리를 이용해 통신
- 생산자 프로세스가 공유 메모리(buffer)에 item을 생산하고 저장하면, 소비자 프로세스가 이를 읽고 소비
- 동기화 필요(Producer-Consumer Problem: 아무것도 없는 상태에서 소비하려하거나 shared memory가 꽉찬 상태에서 생산하려 한다면 문제 발생)
- buffer를 지속적으로 확인하는 monitoring

![image](https://user-images.githubusercontent.com/54051304/207102027-e19e5c99-c8d6-490c-9a91-7452907835ec.png)


---
## :computer: IPC 종류
:heavy_check_mark: 익명 PIPE
- 한쪽 방향으로만 통신이 가능한 반이중 통신
- 파이프는 두 개의 프로세스를 연결하는데 하나의 프로세스는 데이터를 쓰기만 하고, 다른 하나는 데이터를 읽기만 할 수 있음
- 양쪽으로 모두 송/수신을 하고 싶으면 2개의 파이프 만들어야 함
- 매우 간단하게 사용할 수 있다는 장점

:heavy_check_mark: Named PIPE(FIFO)
- 익명 PIPE의 확장된 형태로, 부모 프로세스와 무관한 다른 프로세스도 통신이 가능한 것
- 익명 파이프는 통신할 프로세스를 명확히 알 수 있는 경우에 사용하는 반면(부모-자식 프로세스 간 통신처럼) Named 파이프는 전혀 모르는 상태의 프로세스들 사이 통신에 사용함
- 익명 파이프처럼 읽기/쓰기 동시에 불가
- 전이중 통신을 위해서는 2개의 파이프를 만들어야 함

:heavy_check_mark: Message Queue
- 입출력 방식은 Named 파이프와 동일
- 파이프처럼 데이터의 흐름이 아니라 메모리 공간임
- 사용할 데이터에 번호를 붙이면서 여러 프로세스가 동시에 데이터를 쉽게 다룰 수 있음

:heavy_check_mark: 공유 메모리
- 파이프, 메시지 큐가 통신을 이용한 설비라면, 공유 메모리는 데이터 자체를 공유하도록 지원하는 설비
- 프로세스 간 메모리 영역을 공유해서 사용할 수 있도록 허용
- 프로세스의 메모리 영역은 독립적으로 가지며 다른 프로세스가 접근하지 못하도록 반드시 보호되야한다. 하지만 다른 프로세스가 데이터를 사용하도록 해야하는 상황도 필요할 것이다. 파이프를 이용해 통신을 통해 데이터 전달도 가능하지만, 스레드처럼 메모리를 공유하도록 해준다면 더욱 편할 것이다.
- 프로세스가 공유 메모리 할당을 커널에 요청하면, 커널은 해당 프로세스에 메모리 공간을 할당해주고 이후 모든 프로세스가 해당 메모리 영역을 접근할 수 있음
- 중개자 없이 곧바로 메모리에 접근할 수 있어 IPC 중 가장 빠르게 동작

:heavy_check_mark: 메모리 맵
- 공유 메모리처럼 메모리 공유
- 열린 파일을 메모리에 맵핑시켜서 공유하는 방식(공유 개체가 파일+메모리)
- 주로 파일로 대용량 데이터를 공유할 때 사용

:heavy_check_mark: 소켓
- 네트워크 소켓 통신을 통해 데이터 공유
- 클라이언트와 서버가 소켓을 통해서 통신하는 구조
- 원격에서 프로세스 간 데이터를 공유할 때 사용

---

<br>

참고

- [tech-interview-for-developer IPC(Inter-Process Comminication)](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/IPC(Inter%20Process%20Communication).md)
