# 🧼 거품 정렬(Bubble Sort)

서로 인접한 두 원소의 크기를 비교해 정렬하는 알고리즘

<br>

## 1️⃣ 과정

**(1) 아래와 같은 배열을 오름차순으로 버블 정렬해보자.**

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/fda97fc8-698d-4816-a07f-87c737c8fc78)

<br>

**(1) 0번째 원소 7과, 1번째 원소 5를 비교했을 때  
7이 더 크므로 위치를 바꿔준다.**


**(2) 이후 같은 방식으로 배열의 끝까지 비교해서  
값이 더 크다면 위치를 바꿔준다.**
![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/953f29c8-24ac-4350-8a11-b2022759e59e)


**(3) 0번째 원소였던 7의 배치가 끝났으면  
새로운 0번째 원소가 된 5와, 1번째 원소 1을 비교해  
같은 과정을 다시 반복한다.**

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/edee656e-b910-4600-9917-9319b071d32a)


**(4) 1과 4를 비교해 1이 더 작으므로 위치를 바꾸지 않는다.**

**(5) 이후 3과 4를 비교했을 때 4가 더 크므로 위치를 바꿔준다.**
![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/3ffdab3f-16ad-4ab0-9c76-c4e0244fcc14)


<br>

## 2️⃣ 예제 코드

```

    int i,j, temp;

    for(i=0; i < LEN; i++){
        for(j=0; j < LEN-i-1; j++){
            if(arr[j] > arr[j+1]){    // swap
                temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }

```


## 3️⃣ 시간 복잡도

- 위의 과정을 보면 비교연산을 5회, 4회, 3회, ... 이런 식으로 수행하는 것을 확인할 수 있다.
- 요소의 개수를 n개로 일반화 하면 **(n-1) + (n-2) + (n-3) + ... + 2 + 1** 이 된다.
- 등차수열 공식에 의해 n*(n+1)/2 과 동일하다
- **시간 복잡도 O(n^2)**



## 4️⃣ 특징

- 하나의 배열에서 값을 바꾸는 식으로 동작하므로, **공간 복잡도 O(n)**
- 선택 정렬과 마찬가지로 swap할 때 필요한 임시변수 정도의 추가공간만 필요하므로 **in-place 정렬**이다.
- (n-1), (n-2), ... 1번의 탐색이 필요하므로, **시간 복잡도 O(n^2)**
- 버블 정렬은 동일한 값을 가진 데이터들의 순서가, 원래의 순서와 같이 유지되는 **stable 정렬**이다.

<br>


## 5️⃣ 장단점

### 장점
- 이해하기 쉬우며, 동시에 구현도 간단하다.
- **제자리 정렬 방식(in-place sorting)** 이다.
- **안정 정렬(stable sort)** 이다

<br>

### 단점
- **시간 복잡도가 O(n^2)** 이기 때문에 비효율적이다.
- 정렬이 되어있던 안되어있던, 2개의 원소를 비교하기 때문에  
  **최선,평균,최악의 경우 모두 시간복잡도가 동일하다.**

<br>

<hr>
#### 참고자료
- [[알고리즘] 버블 정렬(거품정렬, Bubble Sort)](https://hongcoding.tistory.com/182)
- [[알고리즘] 버블정렬(bubble sort)이란?](https://code-lab1.tistory.com/21)
- [거품 정렬(Bubble Sort)](https://gyoogle.dev/blog/algorithm/Bubble%20Sort.html)
