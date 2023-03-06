# :pushpin: Blocking/Non-blocking & Synchronous/Asynchronous

![image](https://user-images.githubusercontent.com/69101568/223138141-e8e59d62-3b3e-4d94-b348-65c4b6daf54b.png)

_IBM developerWorks의 2:2 matrix_

## :computer: Blocking & Non-Blocking

:heavy_check_mark: Blocking

- A 함수가 B 함수를 호출할 때, B 함수가 자신의 작업이 종료되기 전까지 A 함수에게 제어권을 돌려주지 않는 것
- 호출된 함수가 제어권을 호출한 함수에게 바로 돌려주지 않으면 Block!

:heavy_check_mark: Non-Blocking

- A 함수가 B 함수를 호출할 때, B 함수가 제어권을 바로 A 함수에게 넘겨주면서, A 함수가 다른 일을 할 수 있도록 하는 것
- 호출된 함수가 바로 제어권을 건네주어(return) 호출한 함수가 다른 일을 진행할 수 있도록 해주면 Non-Block!

---

## :computer: Synchronous & Asynchronous

:heavy_check_mark: Synchronous

- A 함수가 B 함수를 호출 할 때, B 함수의 결과를 A 함수가 처리하는 것
- 호출된 함수의 수행 결과 및 종료를 호출한 함수도 신경 쓰면 Sync!

:heavy_check_mark: Asynchronous

- A 함수가 B 함수를 호출 할 때, B 함수의 결과를 B 함수가 처리하는 것
- 호출된 함수의 수행 결과 및 종료를 호출된 함수 혼자 신경쓰면 Aync!

---

## :computer: 2:2 Matrix로 확인하는 4가지 모델

_**Blocking과 Non-Blocking은 함수를 호출하고 그 처리가 끝날 때가지 기다리는지 안기다리는지 차이**_
_**Sync와 Aync는 함수를 호출하고 그 결과를 받을 때 그 결과와 순서에 관심이 있는지 없는지 차이**_

:heavy_check_mark: **Blocking & Sync / Non-blocking & Async**

![image](https://user-images.githubusercontent.com/69101568/223143357-81d22cf2-7c69-4f65-832e-8d86b3daedb0.png)

- Blocking & Sync 예시
  - client가 server에게 request 보내고 reponse를 기다림
  - 만약 server가 다른 requests 처리로 바쁘다면 client는 response를 받을 때까지 기다림 (block됨)
- Non-blocking & Async 예시
  - client가 큰 파일을 전송하기 위해서 server에게 request를 보냄
  - client는 파일이 백그라운드에서 전송되는 동안 다른 처리를 할 수 있음

:heavy_check_mark: Non-blocking & Sync

![image](https://user-images.githubusercontent.com/69101568/223145286-646457f4-9055-465c-9a21-22839e064b65.png)

- Non-blocking & Sync 예시
  - client가 server에게 request 보내고 reponse를 기다림
  - 만약 server가 바쁘면 client는 다른 일을 계속하고 server로 부터 response가 왔는지 주기적으로 체크

:heavy_check_mark: Blocking & Async

![image](https://user-images.githubusercontent.com/69101568/223145769-61018cb1-1b5d-431c-b42b-39c87a1b7e2d.png)

- Blocking & Async 예시
  - client가 큰 파일을 전송하기 위해서 server에게 request를 보냄
  - client는 전송이 완료되기를 기다릴 필요 없이 다른 일을 계속 할 수 있음
  - 하지만 전체 파일이 전송되기까지 전송 프로세스 그 자체는 block
  - ~~이 조합은 별로라서 잘 사용 안한대...~~

---

<br>

참고

- [Sync/Async, Blocking/Non-Blocking 무슨 차이일까?](https://velog.io/@maketheworldwise/SyncAsync-BlockingNon-Blocking-%EB%AC%B4%EC%8A%A8-%EC%B0%A8%EC%9D%B4%EC%9D%BC%EA%B9%8C)
- [Blocking, Non-Blocking, Sync, Async의 차](https://jh-7.tistory.com/25)
- [동기와 비동기, 그리고 블럭과 넌블럭](https://musma.github.io/2019/04/17/blocking-and-synchronous.html)
