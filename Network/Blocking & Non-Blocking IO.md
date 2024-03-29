
# 📌 Blocking & Non-Blocking I/O


### I/O가 성능에 미치는 영향
- **I/O** : 데이터의 입력(Input)과 출력(Output)
- 어떤 디바이스(or 네트워크)를 통해 입출력(or 송수신)이 이뤄지는 작업
- User 레벨에서 직접 수행할 수 X  
  _( 실제 수행 위치 : Kernel(운영체제) )_
- 유저 프로세스(or 스레드)는 커널에게 요청 → 작업 완료 후 → 커널에 반환하는 결과를 기다릴 뿐


## 🏸 blocking I/O란?

- 가장 기본적인 I/O 모델

- I/O작업이 진행되는 동안 유저 프로세스가 자신의 작업을 중단한 채,  
I/O가 끝날때까지 대기하는 방식
 



![image](https://user-images.githubusercontent.com/63834758/225175428-f9e6e90e-f328-4dc7-a99b-aed3695471eb.png)


> 1. 유저(application)는 Read()를 호출해 → 커널에게 read I/O작업을 요청 (제어권을 넘겨준다)  
> 
> 2. 데이터가 입력될 때 까지 대기   
> (제어권을 넘겨주었기 때문에 대기한다. 자기 작업을 제어할 수 없다.)  
> application은 block이 되어 다른 작업을 하지 못한다.
> 
> 3. 데이터가 입력되면 유저에게 결과가 전달되어야만 유저 자신의 작업에 비로소 복귀할 수 있다.  
>     (제어권을 넘겨받는다)  
>     - 이는 read I/O가 수행될 때까지는 어플리케이션이 다른 작업을 수행하지 못한다는 것을 의미
>     - 말그대로 block이 되고, 어플리케이션에서 다른 작업을 수행하지 못하고 대기하게 되므로, 자원 낭비



## 🏸 non blocking I/O란?

- blocking방식의 비효율성을 극복하고자 도입된 방식
- A함수가 I/O작업을 호출했을 때  
I/O작업이 완료될까지 A함수의 작업을 중단하지 않고  
I/O 호출에 대해 즉시 리턴 → A함수가 이어서 다른 일을 수행할 수 있도록 하는 방식
 

![image](https://user-images.githubusercontent.com/63834758/225175461-2d46f56d-043b-4b53-b70c-5302e3e9a333.png)


- EWOULDBLOCK → 데이터가 없다는 메시지


> 1. 유저가 커널에게 read작업(System Call)을 요청하면
>
> 2. 커널의 I/O작업 완료 여부와는 무관하게 즉시 응답한다. (즉시 결과 반환)  
>    이때 입력 데이터가 없으면 입력 데이터가 없다는 결과 메세지 (EWOULDBLOCK)을 반환
>        - 이는 커널이 System Call을 받자마자 CPU 제어권을 다시 application에게 넘겨주는 것이다.  
>        - application : I/O 작업이 완료되기 전에 다른 작업 수행 가능
>        - 중간중간 System Call을 보내서 I/O가 완료됐는지 커널에게 물어보고, 완료되면 I/O작업을 완료한다.
>    
> 3. 입력 데이터가 있을 때 까지 1,2번을 반복한다.  
>    → 2번에서 결과 메세지를 받은 유저는 다른 작업진행이 가능하다.  
>    
> 4. 입력데이터가 있으면 유저에게 결과가 전달된다.   
>    - 이 경우 I/O의 진행시간과 관계가 없기 때문에  
>      application에서 작업을 오랜 시간 중지하지 않고 I/O작업 진행 가능
>   - 그러나 반복적으로 시스템 호출이 발생하기 때문에 이 경우 역시 자원 낭비 O


<hr>

### 참고자료

- [blocking I/O, non-blocking I/O에 대하여](https://etloveguitar.tistory.com/m/140)
- [Blocking I/O 와 Non-Blocking I/O](https://didu-story.tistory.com/307)
