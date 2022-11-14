# 📌 B Tree & B+ Tree

## 👉 1. B Tree와 B+ Tree

   - 개요 
   
      - 데이터 베이스와 파일 시스템에서 널리 사용 되는 자료구조
      - 이진 트리를 확장해 자식 노드의 최대 숫자가 2보다 큰 트리 구조
      - 데이터가 정렬된 상태로 유지되어 있음
      - MySQL의 DB엔진인 InnoDB가 B+ Tree로 이루어짐
      - 참고) 트리 구조
      
         ![image](https://user-images.githubusercontent.com/101535851/201673607-50266207-6247-466d-88a6-61b8a1fbd92a.png)


# 🌲 2. B Tree

   ![image](https://user-images.githubusercontent.com/101535851/201680447-e1e83163-4de4-4236-a6f7-49e49cc5dd84.png)

   1. 개요
      
      - B Tree는 Binary search tree와 유사하지만 한 노드 당 자식 노드가 2개 이상 가능
      - key값을 이용해 찾고자 하는 데이터를 트리 구조를 이용해 찾는 것
   
   2. B Tree는 왜 빠른가?
      
      - 어떤 값에 대해서도 같은 시간에 결과를 얻을 수 있는 '균일성'이 보장
      - 트리의 높이가 다른 경우 약간의 차이는 있지만 O(logN)이라는 시간 복잡도를 구할 수 있음
      - ex) 8과 30을 찾는 시간은 동일
      
   3. B Tree는 균형 트리다
   
      ![image](https://user-images.githubusercontent.com/101535851/201674449-ee64983c-2c6b-4bc1-a36b-49311cba7927.png)   
      - 균형 트리
         - 루트로부터 리프까지의 거리가 일정한 트리 구조
         - 트리 중에서 성능이 특히 안정화되어있음
      
      - 첫 생성 당시 균형 트리
      - 테이블 갱신(insert/update/delete) 반복을 통해 서서히 균형이 깨지며 성능이 악화됨
      - 어느정도는 자동으로 균형을 회복하는 기능이 있음
      - 그러나, 갱신 빈도가 높은 테이블에 작성되는 인덱스의 경우 인덱스 재구성을 해 트리의 균형 되찾는 작업 필요
      


# 🎄 3. B+ Tree


   ![image](https://user-images.githubusercontent.com/101535851/201680136-e695ae3d-4dd8-456a-873c-ef10f09e6ba3.png)

   1. 개요
      
      - B Tree의 확장 개념
      - 브랜치 노드에 key만 담아두고 data는 담지 않음
      - 오직 리프 노드에만 key와 data를 저장
      - 리프 노드에만 data가 저장되기 때문에 리프 노드의 부모 노드에는 리프 노드의 키가 일부 저장됨
      - 같은 레벨 노드끼리 서로 연결되어 있음

   2. 장점
      
      - 리프노드에만 데이터를 담아 두기 때문에 메모리를 더 확보함으로써 더 많은 key 수용 가능
      - 풀스캔시 B+ Tree는 리프 노드에 데이터가 있기 때문에 한번의 선형 탐색만 하면 됨 (B-Tree는 모두 확인)

   3. 단점
   
      - B-Tree 최상의 케이스에서는 루트에서 끝날 수 있으나 B+ Tree는 무조건 리프까지 내려가야 함

   5. InnoDB
      
      ![image](https://user-images.githubusercontent.com/101535851/201676552-d5be8a47-89b4-469b-b2c5-1aafecc83c86.png)

## 🌟 4. B Tree vs B+ Tree (면접 질문으로 가끔 나옴)

   | 구분 | B Tree | B+ Tree |
   |-|-|-|
   | 데이터 저장 | 리프, 브랜치 모두 저장 가능 | 리프만 가능 |
   | 트리의 높이 | 높음 | 낮음(한 노드 당 key를 많이 담을 수 있음) |
   | 풀 스캔 시, 검색 속도 | 모든 노드 탐색 | 리프 노드에서 선형 탐색 |
   | 키 중복 | 없음 | 있음 |
   | 검색 | 자주 access 되는 노드를 루트 노드 가까이 배치 => 브랜치 노드에도 데이터가 존재할 수 있어 빠름 | 리프 노드까지 가야만 데이터 존재 |
   | 링크드 리스트 | 없음 | 리프 노드끼리 링크드 리스트로 연결 |
   
   -  차이점 중 가장 중요한 것
   
      1. B Tree의 각 노드에서는 key 뿐만 아니라 data도 들어갈 수 있다
      2. B+Tree는 각 node에서는 key만 들어가야 한다. 그러므로 B+Tree에서는 data는 오직 leaf에만 존재
      3. B+Tree는 B-Tree와는 달리 add, delete가 leaf에서만 이루어진다.
      4. B+ Tree는 leaf node끼리 linked list로 연결되어 있다.
   
 ## 💿 5. 유용한 이유: 디스크에 대해 알아보자

   1. 디스크 구조
   ![image](https://user-images.githubusercontent.com/101535851/201664673-64e05655-5971-4b46-baaf-68b55fec2b1e.png)
      - 트랙: 그림에서 빨간색으로 색칠된 영역
      - 섹터: 원을 피자로 봤을 때 잘라낸 한 조각
      - 블록: 트랙과 섹터의 교집합
      
   2. 디스크 읽고/쓰기
         
      - 블록 단위로 이루어짐
      - 데이터에 접근 시 회전을 통해 섹터를 찾고 헤드를 앞위로 움직이며 트랙을 찾음
      - 핵심은 특정 데이터를 찾기 위해 탐색해야 하는 블록의 수를 줄이는 것!!!

   3. 디스크에 데이터가 저장되는 방식

      - ex) 하나의 row가 128 byte인 데이터 100개 저장 
      
         |eid|name|dept|section|add|
         |-|-|-|-|-|
         |10 bytes|50 bytes|10 bytes|8 bytes|50 bytes|
      - 디스크의 블록 사이즈 = 512 byte
         -  하나의 블록에 4개의 row 저장 가능
         -  100개의 row를 저장하기 위해서는 25개의 블록 필요
         -  특정 row를 찾기 위한 최악의 경우 25개의 블록을 모두 살펴야 함
         -  `select * from employee where eid=1`

   4. 인덱스
   
      - 대용량 테이블에서 필요한 데이터만 빠르고 효율적으로 엑세스하기 위해 사용하는 오브젝트
      - ex) eid와 해당 row를 가리키는 포인터로 구성된 인덱스 구성
         |eid|pointer|
         |-|-|
         |10 bytes|6 bytes|
      - 디스크의 블록 사이즈 = 512 byte
         - 하나의 블록에 32개 index 저장 가능
         - 100개의 데이터에 대한 index이므로 4개의 블록 필요
         - 즉, 4개의 블록만 살핀 다음 row의 주소를 따라서 1개의 블록만 더 살피면 됨
         - 이전 방법보다 상당히 줄어듦

   5. 멀티 레벨 인덱스
   
      - 데이터가 많아서 인덱스의 크기가 커지고 인덱스를 찾는 과정이 부담스러워진다면?
      - row를 찾기 위한 인덱스를 만들었듯이 인덱스를 위한 인덱스를 만듦
      - 이것이 멀티 레벨 인덱스
      ![image](https://user-images.githubusercontent.com/101535851/201670920-28b678f1-ec06-4098-a9b5-8e6b1f440b5b.png)

### 참고
   - [데이터베이스에서 B 트리(B+ 트리)가 유용하게 쓰일 수 있는 이유](https://live-everyday.tistory.com/243)
   - [[Computer Science] B-트리(B-Tree) 삽입 삭제](https://kunduz.tistory.com/entry/Computer-Science-B-%ED%8A%B8%EB%A6%ACB-Tree)
   - [[MySQL] B-tree, B+tree란? (인덱스와 연관지어서)](https://zorba91.tistory.com/293)
   - [B-Tree, B+ Tree](https://ssup2.github.io/theory_analysis/B_Tree_B+_Tree/)

