# ✨ Index

## 📌 1. Index란?

- 추가적인 저장 공간을 활용해 테이블 검색 속도를 높이기 위한 기술
- [B Tree와 B+ Tree 구조가 가장 많이 사용](https://github.com/SeoYeonBae/CS_study/blob/main/DataStructure/B%20Tree%20%26%20B%2B%20Tree.md)

## ✔ 2. Index 생성 & 검색 과정

### 1️⃣ 생성

  1. 특정 컬럼에 인덱스를 생성
  2. 해당 컬럼의 **데이터를 정렬**하여 별도의 메모리 공간에 데이터의 물리적 주소와 함께 저장

### 2️⃣ 검색

  1. 인덱스 생성 컬럼을 where 조건으로 검
  2. 인덱스에 저장되어 있는 데이터의 물리적 주소로 가서 데이터를 가져옴

![image](https://user-images.githubusercontent.com/101535851/213040840-ca443885-a6f6-444a-93cc-65aa5882f071.png)

## ✔ 3. Index의 사용 이유 = 장점

> ❗ 인덱스의 가장 큰 특징은 데이터가 정렬되어있다는 점을 기억 ❗

### 1️⃣ 조건 검색 where절의 효율성

   - 테이블을 만들고 데이터가 쌓이게 되면 레코드는 내부적으로 순서 없이 뒤죽박죽 저장됨 -> 검색 조건 풀스캔
   - 인덱스 테이블 사용 시 데이터가 정렬되어 있어 조건에 맞는 데이터를 빠르게 찾아낼 수 있음
   - 즉, 속도가 향상됨

### 2️⃣ 정렬 order by 절의 효율성

  - order by는 부하가 많이 걸리는 작업
  - 정렬과 동시에 1차적으로 메모리에서 정렬이 이루어지고 메모리보다 큰 작업이 필요하면 디스크 I/O(데이터 작성 변경 시 HDD에 저장)도 추가적으로 발생되기 때문
  - 인덱스 테이블 사용 시 이미 정렬되어 있기 때문에 가져오기만 하면 돼서 전반적인 자원 소모를 안 해도 됨

### 3️⃣ min, max의 효율적인 처리

  - 데이터가 이미 정렬되어 있어서 시작값과 끝값만 가져오면 됨
  - 풀스캔보다 훨씬 효율적

## 4. Index의 단점

> ❗ 인덱스의 가장 큰 문제는 정렬된 상태를 계속 유지시켜 줘야 한다는 것 ❗

### 1️⃣ DML에 취약

  - insert, update, delete를 통해 데이터가 추가되거나 값이 바뀌면 인덱스 테이블 값을 다시 정렬해야 함
  - 또한, 인덱스 테이블과 원본 테이블 두 곳의 데이터 수정 작업을 해 줘야 함
  - DML이 빈번한 테이블 보다는 검색 위주의 테이블에 인덱스를 생성하는 것이 효과적

#### 1-1. insert
    
  - 인덱스의 block들이 하나에서 두 개로 나누어지는 현상인 insert split이 발생 할 수 있음
  
  - ex) 블록이 이미 꽉 차있는데 새로운 데이터를 블록에 저장해야하는 상황

  ![image](https://user-images.githubusercontent.com/101535851/213051256-00468707-b2a2-4a22-acb4-9be3b887ebbe.png)
  
  - 아래와같이 일부 데이터를 새로운 블록에 보내버리고 데이터를 받아들임

  ![image](https://user-images.githubusercontent.com/101535851/213051433-7b70efd9-ba24-478c-b7c8-98b61baf7a97.png)
    
  - 이게 무엇이 문제인가!
  
    - *Redo : DataBase에서 일어난 모든 변화를 저장하는 메모리 공간
    - 새로운 블록을 할당받아야되고...키도 옮겨야하고...Redo에 모든수행 과정이 기록되어야하고... 후 할일이 너무많다
    - 스플릿이 이루어지는 동안 키 값을 보호하기 위해서  DML(삽입,삭제,검색,갱신) 이 블로킹됨
    
#### 1-2. delete

  - Table에서 data가 delete 되는 경우 : Data가 지워지고, 다른 Data가 그 공간을 사용 가능
  - Index에서 Data가 delete 되는 경우 : Data가 지워지지 않고, 사용 안 됨 표시만 해둠
  - Table의 Data 수와 Index의 Data 수가 다를 수 있음

#### 1-3. update

  - Table에서 update가 발생하면 -> Index는 Update 할 수 없음
  - Index에서는 Delete가 발생한 후, 새로운 작업의 Insert 작업 / 2배의 작업이 소요

### 2️⃣ 그렇다면 무조건 검색 시에 효과적?

  - 인덱스는 전체 데이터 중에서 10-15% 이하의 데이터 처리에만 효율적
  - 그 이상의 데이터 처리엔 사용하지 않는 것이 좋음
  - ex) 1개의 데이터가 있는 테이블과 100만개의 데이터가 있는 테이블이 있을 때
      
      - 100만개의 테이블이라면 풀스캔보단 인덱스 스캔이 빠르지만 1개의 데이터가 있는 테이블은 풀스캔이 빠를 것

### 3️⃣ 저장 공간의 필요성

  - 인덱스 관리를 위해서는 데이터베이스의 약 10%에 해당하는 저장공간 필요

## 5. Index를 사용하면 좋은 경우와 피해야 하는 경우

### 1️⃣ Index를 사용하면 좋은 경우

  - where 절에서 자주 사용되는 column
  - 외래키가 사용되는 column
  - join에 자주 사용되는 column
  - = 으로 비교되는 cloumn
  - order by 절에서 자주 사용되는 column


#### 2️⃣ Index 사용을 피해야 하는 경우
  
  - data 중복도가 높은 column
  - dml이 자주 일어나는 column


---

#### 참고

- [Index](https://gyoogle.dev/blog/computer-science/data-base/Index-.html)
- [DB Index 란?](https://lalwr.blogspot.com/2016/02/db-index.html)
- [데이터베이스(DB) 인덱스(Index) 란 무엇인가?](https://choicode.tistory.com/27)
- [데이터베이스 인덱스를 알아보자](https://weejw.tistory.com/131)
