## 선택 정렬(Selection Sort)

### 💡 개념

- 정렬되지 않은 데이터들에 대해 가장 작은 데이터를 찾아 가장 앞의 데이터와 교환해나가는 방식
- 가장 큰 데이터를 찾아 가장 뒤의 데이터와 교환하는 것과 동일

### 📈 과정

![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/1c0d5763-42cb-4a26-9e70-50ebfbc959a7)


1. 배열에서 가장 큰 원소를 찾는다.
2. 배열의 끝자리에 있는 원소와 자리를 바꾼다.
3. 배열의 끝자리를 제외한 나머지 원소들로 같은 작업을 반복한다.

*가장 작은 원소를 찾아 배열의 맨 앞자리에 놓는 것과 동일한 과정*

### 💻 구현
```java
public static int theLargest(int[] A, int last) {
      int largest = 0;
      for(int i = 1; i <= last; i++) {
          if(A[i] > A[largest])
              largest = i;
      }
      return largest;
}

public static void selectionSort(int[] A, int n) {
    //  n  :  A.length
    int largest = -1;

    // 1.
    for(int last = n; last > 0; last--) {

        //  2.
        largest = theLargest(A, last);

        //  3.
        int temp = A[largest];
        A[largest] = A[last];
        A[last] = temp;
    }
}
```

### ⏱ 시간 복잡도
선택 정렬의 수행 시간은 모든 경우에 `O(n^2)`로 항상 일정한 시간 복잡도를 가진다.
1. for문 n-1번 순환
2. 가장 큰/작은 수를 찾는 작업이므로 부분 배열의 크기에 비례한다
    - 크기가 k인 배열에서 가장 큰/작은 수를 찾는 데는 k-1번의 비교
     - 부분 배열의 크기는 n부터 2까지, 즉 (n - 1) + (n - 2) + ... + 2 + 1 = n(n-1)/2 그러므로 `O(n^2)`
3. 두 원소를 교환하는데 상수 시간 소요
 **수를 비교하는 횟수가 전체 시간을 좌우한다.**

### 😊 장점
- 알고리즘이 단순하다.
- 정렬을 위한 비교 횟수가 많지만, 거품 정렬에 비해 실제 교환하는 횟수가 적기에 많은 교환이 일어나는 경우 효율적이다.
- 정렬이 진행됨에 따라 속도가 빨라지는 속성을 지니기에  같은 `O(n^2)`여도 거품 정렬보다 조금 더 빠르다.


### 😥 단점
- 시간 복잡도가 항상 `O(n^2)`로 퀵, 삽입 정렬에 비해 속도가 느린 편이다.

<hr>

### 참고
- [선택정렬(Selection Sort)이란?](https://ssdragon.tistory.com/110)
- [선택 정렬](https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC)
