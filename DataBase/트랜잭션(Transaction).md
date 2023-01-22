# :pushpin: 트랜잭션(Transaction)

## :computer: 트랜잭션이란???

_데이터베이스의 상태를 변환시키는 하나의 논리적 기능을 수행하기 위한 작업의 단위 또는 한꺼번에 수행되어야할 일련의 연산들을 의미한다_

:heavy_check_mark:  데이터베이스의 상태를 변환시키는 것

- SELECT
- INSERT
- DELETE
- UPDATE
   
:heavy_check_mark:  트랜잭션의 역할

- 트랜잭션은 **작업의 완전성**을 보장해준다
- 논리적인 작업 셋을 모두 완벽하게 처리하거나 또는 처리하지 못할 경우에는 원 상태로 복구해서 작업의 일부만 적용되는 현상이 발생하지 않게 만들어준다

---

## :computer: 트랜잭션의 성질 (ACID)

- **A**tomicity(원자성)
  - 트랜잭션의 연산은 데이터베이스에 모두 반영이 되든지 아니면 전혀 반영이 되지 않아야 함
  - 연산이 완벽하게 수행되지 않고 어느 하나라도 오류가 발생하면 트랜잭션 전부가 취소되어야 함
- **C**onsistency(일관성)
  - 트랜잭션의 작업 처리 결과가 항상 일관성이 있어야 함
- **I**solation(독립성)
  - 둘 이상의 트랜잭션이 동시에 실행되고 있을 경우 어떤 하나의 트랜잭션이라도 다른 트랜잭션의 연산에 끼어들 수 없음
- **D**urability(지속성)
  - 트랜잭션이 성공적으로 완료되었을 경우, 결과는 영구적으로 반영되어야 함
  
---

## :computer: 트랜잭션의 연산과 상태

:heavy_check_mark:  트랜잭션의 연산

- Commit 연산
  - 하나의 트랜잭션이 성공적으로 끝났고, 데이터베이스가 일관성있는 상태에 있을 때 하나의 트랜잭션이 끝났음을 알려주기 위해 사용하는 연산
- Rollback 연산
  - 하나의 트랜잭션 처리가 비정상적으로 종료되어 데이터베이스의 일관성을 깨뜨렸을 때, 이 트랜잭션 일부가 정상적으로 처리되었더라도 원자성을 구현하기 위해 이 트랜잭션이 행한 모든 연산을 취소하는 연산

:heavy_check_mark:  트랜잭션의 상태

![image](https://user-images.githubusercontent.com/69101568/213923158-aaab8ae6-c887-4f97-836b-672048a75e7e.png)

- 활동 : 트랜잭션이 실행중인 상태
- 부분완료 : 트랜잭션의 마지막 연산까지 실행했지만 Commit 연산이 실행되기 직전의 상태
- 완료 : 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태
- 실패 : 트랜잭션 실행에 오류가 발생하여 중단된 상태
- 취소 : 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태

---

<br>

참고

- [[DB]트랜잭션(Transaction)이란? ACID란?](https://code-lab1.tistory.com/51)
- [[DB기초]트랜잭션이란 무엇인가?](https://coding-factory.tistory.com/226)
- [DB 트랜잭션(Transaction)](https://gyoogle.dev/blog/computer-science/data-base/Transaction.html)