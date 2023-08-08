## 최소 공통 조상(LCA)

### 개념
- *Lowest Common Ancestor*
- 트리 구조에서 임의의 두 정점이 갖는 **가장 가까운 조상 정점**을 의미한다.

### 흐름
1. 모든 노드에 대한 깊이를 계산한다.
2. 최소 공통 조상을 찾을 두 노드를 확인한다.
3. 먼저 두 노드의 깊이가 동일하도록 거슬러 올라간다.
4. 부모가 같아질 때까지 반복적으로 두 노드의 부모 방향으로 거슬러 올라간다.
5. 모든 LCA(a,b) 연산에 대하여 3 ~ 4 번의 과정을 반복한다.

### 구현 방법

### DFS + DP
- parent 배열을 **2차원**으로 선언한다.
  - parent[a][b] : a번 정점의 2^b번째 조상 노드
 

    - **왜 2의 거듭제곱으로 조상 노드를 나타낼까?**
    - 2의 거듭제곱 수들의 합으로 모든 양의 정수를 표현할 수 있기 때문
    - ex. 3칸 위에 있는 조상 노드를 찾고 싶다면 *2^0번쨰 조상의 2^1번째 조상 찾기*
  - parent[a][b] = parent[parent[a][b-1]][b-1]
    - DFS를 통해 root부터 트리를 구성한다면 낮은 깊이의 노드부터 탐색하기 때문
       
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/5b8467dd-c3c9-4168-bc5f-c19d26a750ea)
              
### 🔎 예 ) 13과 7의 LCA 구하기                       
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/17ffcf7d-bc58-48e1-b573-979b4b1862a2)

#### 1. depth가 더 깊은 노드를 depth가 같아지도록 조상을 찾아 올라가기
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/7ae6b513-599d-4d7f-99a2-77611ab5a177)
- 13의 depth는 4로 7의 depth보다 깊기에 depth가 *동일하게* 4가 되도록 조상을 찾아 올라간다.

#### 2. 두 노드가 같은지 비교하고 만약 다르다면 같아질 때까지 올라가기
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/ec2d75d3-e751-4b6b-827f-6441b17f3495)              
           
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/9440f670-a6dc-4267-9b5c-e08b57d32882)

### 코드
```java

```

### ⏲ 시간 복잡도
**`O(logN)`**
- 조상을 향해 하나씩 올라가는 것이 아닌 2의 제곱수만큼 올라가기에 시간복잡도가 `O(logN)`로 줄어든다.

### 참고
- [[알고리즘] LCA 알고리즘 정리](https://stg0123.github.io/algorithm/29/)
- [](https://4legs-study.tistory.com/121)
