# 📌 해시(Hash) - 해시 함수와 해시 테이블


## ✔️ 1. 개요

   - 해시 함수란?

      - 데이터의 효율적 관리를 목적으로 임의의 길이 데이터를 고정된 길이 데이터로 매핑하는 함수
      
   - 특징
   
      - 어떤 입력 값에도 항상 고정된 길이의 해시값을 출력
      - 동일한 값이 들어오면 언제나 동일한 값 출력
      - [해시 생성기](https://www.convertstring.com/ko/Hash/SHA256)

   - 주요 단어

      - key: 매핑 전 원래 데이터의 값
      - hash-value: 매핑 후 데이터의 값
      - hashing: 매핑하는 과정 자체
      - hash table: 해시값을 index나 주소로 사용해 데이터의 값을 키와 함께 저장하는 자료 구조
      - bucket: 해시 테이블의 각 엔트리, 쉽게 말하면 해시 테이블의 행
      - slot: 버켓의 단위, 쉽게 말하면 해시 테이블의 열

 ![image](https://user-images.githubusercontent.com/101535851/200308623-cb6972ed-7892-4fad-8eda-1b777864c2ef.png)
 
 |Index(Hash Value)|Data|
 |-|-|
 |01|(Lisa Smith, 521-8976)|
 |02|(Jhon Smith, 521-1234)|
 |...|...|
 
## ✔️ 2. 해시 테이블의 장점

   - 데이터의 효율적인 관리

      - 하드디스크나 클라우드에는 무한에 가까운 데이터가 존재
      - 이를 유한한 개수의 해시값으로 매핑하면 작은 크기의 메모리로 프로세스를 관리할 수 있음
   
   - index(색인) 사용 가능
      
      - index를 안다면 빠르게 접근 가능
      - 삽입, 삭제, 탐색시 O(1)의 시간복잡도를 보임

   - 보안 분야에서 널리 사용 가능

      - 키와 해시 사이에 직접적인 연관이 없어 해시값만으로 키를 온전히 복원하기 어려움
 

## ✔️ 3. 해시 테이블의 충돌

![image](https://user-images.githubusercontent.com/101535851/200306407-471beb53-a729-4fdf-991b-e0cac95e0ea9.png)

   - collision 현상
      
      - 데이터가 많아지면 다른 데이터가 같은 해시값으로 충돌나는 현상 발생

   - 충돌 해결 방법

      1. 체이닝
         - 버킷에 데이터가 이미 있다면 연결리스트로 노드를 계속 추가하는 방식
         - 제한 없이 계속 연결 가능해 유연한 방법이지만, 메모리 문제가 있음
         - ![image](https://user-images.githubusercontent.com/101535851/200310074-797b720a-ed4b-4598-b447-2ca2a8c4aebf.png)

      2. Open Addressing
         - 해시 함수로 얻은 주소가 아닌 다른 주소에 데이터를 저장할 수 있도록 허용하는 방식
         - 그림을 예시로 봤을 때 키가 7로 나눈 나머지로 정의했다면 충돌 문제가 발생할 수 있음
         - 특정 해시값에 키가 몰리면 효율성이 크게 떨어짐
         - ![image](https://user-images.githubusercontent.com/101535851/200311047-125d6d66-5f85-438c-8f12-c08982fd61de.png)

      3. 선형 탐사
         - 최초 해시값에 해당하는 버킷에 다른 데이터가 저장되어 있으면 정해진 고정폭으로 이동하는 방식
         - 그림은 고정폭 1의 선형 탐사
         - ![image](https://user-images.githubusercontent.com/101535851/200311399-e6cbf001-2722-458a-86ba-06b648ac6937.png)

      4. 제곱 탐사
         - 최초 해시값에 해당하는 버킷에 다른 데이터가 저장되어 있으면 정해진 고정폭을 제곱수로 이동하는 방식
         - 그림은 고정폭 1의 제곱 탐사
         - ![image](https://user-images.githubusercontent.com/101535851/200315464-5e9f7967-b6ba-4395-9d81-7169d0f0b07e.png)

---

참고

- [해시(Hash)](https://gyoogle.dev/blog/computer-science/data-structure/Hash.html)
- [해싱, 해시함수, 해시테이블](https://ratsgo.github.io/data%20structure&algorithm/2017/10/25/hash/)
