# 🏍 퀵 정렬(Quick Sort)

  
다른 원소와의 비교만으로 정렬을 수행하는 불안정 정렬.  
분할 정복 알고리즘의 하나로, 평균적으로 매우 빠른 수행 속도를 가진다.

<br>

> [분할 정복(divide and conquer)]
> 
> 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음,  
> 결과를 모아서 원래의 문제를 해결한다. 대개 순환 호출을 이용하여 구현

<br>

## 1. 과정 

 1. 리스트 안에 있는 **한 요소를 선택**한다.  
    이렇게 고른 원소를 **pivot(피벗)** 이라고 한다.  

<br>

 2. pivot을 기준으로 **pivot보다 작은 요소**들은 모두 pivot의 왼쪽으로 옮기고  
    **pivot보다 큰 요소**들은 모두 pivot의 오른쪽으로 옮긴다.

<br>

 3. **pivot을 제외한** 왼쪽 리스트와 오른쪽 리스트를 **다시 정렬**한다.  
  3-1) 분할된 왼쪽 리스트와 오른쪽 리스트도 **다시 pivot을 정하고** pivot을 기준으로 2개의 부분리스트로 나눈다.  
  3-2) 재귀를 사용하여 부분 리스트들이 더이상 **분할이 불가능 할 때까지 반복**한다.  

<br>

## 2. 예시

### (1) pivot 설정

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/888cd590-7bd3-4994-9012-48f06233e1e4)

- 위와 같은 배열을 오름차순으로 퀵 정렬 한다고 하자.
- 가장 먼저 **pivot을 설정**
    - pivot을 설정하는 것에는 여러가지 방법이 있다.
    - **가장 앞의 원소, 중간 원소, 혹은 가장 뒤의 원소를** 택하는 등
- 여기서는 중간 원소를 pivot값으로 설정하는 것을 택하겠다.

<br>

### (2) left와 right 분할

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/ceff46e7-7ed4-4e10-8acf-ed3f04a2981b)

- **가장 왼쪽의 값을 left, 오른쪽의 값을 right로** 잡는다. (여기서 L은 배열의 가장 왼쪽, R은 가장 오른쪽의 위치를 나타낸다) 
- left는 오른쪽으로, right는 왼쪽으로 이동
    - 이 때 **left**는 pivot보다 큰 수를 만나거나 pivot을 만나면 멈추고, 
    - **right**는 pivot보다 작은 수를 만나거나 pivot을 만나면 멈춘다.
- 따라서 5가 3보다 크므로 left는 5에서 멈추고, 2가 3보다 작으므로 right는 2에서 멈춘다.


<br>

### (3) left와 right 교환

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/f5a53905-49dc-4dba-827c-dc1d38733f41)

- left와 right가 멈췄을 때, **left가 right보다 왼쪽에 있다면** left와 right 값을 교환
- 이후 left를 **오른쪽으로 한 칸**, right를 **왼쪽으로 한 칸** 이동
- 위 과정을 **left가 right 보다 오른쪽으로 올 때까지** 반복

<br>


### (4) left와 right 교환

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/bc272ec2-7707-415b-8492-aad61842b3a3)

- 6이 3보다 크므로 6에서 left가 멈춘다.
- right는 pivot을 만나서 멈춘다. 
- 이 때 left가 right보다 왼쪽에 있으므로 **left와 right 값을 교환**
- left를 오른쪽으로 한 칸, right를 왼쪽으로 한 칸 이동
- **left 가 right 보다 오른쪽에 있으므로 종료**

<br>


### (5) 재귀

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/dc41b2ac-e11d-4247-a7cc-a97f686450f7)

- **right가 L보다 크다면** L부터 right까지 다시 위 과정을 재귀적으로 반복
- **left가 R보다 작다면** left부터 R까지 다시 위 과정을 재귀적으로 반복

<br>

### (6) 배열 정렬

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/6a38bf28-ab9d-424b-a21a-cb81594f27ef)

- **왼쪽 부분 배열 정렬 과정**
    - left는 2에서 멈춘다.
    - right는 pivot에서 멈춘다.
    - **left가 right보다 왼쪽에 있으므로** 둘을 교환한다.
    - left를 오른쪽으로 한 칸, right를 왼쪽으로 한 칸 이동한다.
    - **left가 right보다 오른쪽에 있으므로 종료한다.**
    - 이때 **right가 L보다 크지 않으므로** 왼쪽배열(L부터 right)은 다시 재귀적으로 정렬할 필요가 없다.
    - left는 R보다 작으므로 **left부터 R까지 다시 재귀적으로** 정렬을 수행한다. 

- **오른쪽 부분 배열 정렬 과정**
    - left는 6에서 멈춘다.
    - right는 pivot에서 멈춘다.
    - left가 **right보다 왼쪽에 있으므로** 둘을 교환한다.
    - left를 오른쪽으로 한 칸, right를 왼쪽으로 한 칸 이동한다.
    - **left가 right보다 오른쪽에 있으므로** 종료한다.
    - 이때 **right가 L보다 크지 않으므로** 왼쪽배열(L부터 right)은 다시 재귀적으로 정렬할 필요가 없다.
    - left는 R보다 작으므로 **left부터 R까지 다시 재귀적으로** 정렬을 수행한다.

- 이 후 과정도 동일하므로 생략

<br>


### (7) 완료

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/e5335bac-29b8-4c91-90ae-e2ef2192f931)

이와 같은 과정을 거치면 배열이 오름차순으로 정렬된다.


## 3. 예제 코드

```
public class QuickSort {

  public static void main(String[] args) {
    int[] arr = { 3, 1, 5, 6, 20, 10, 7, 11, 15, 9 };
    quickSort(arr);
  }

  public static void quickSort(int[] arr) {
    quickSort(arr, 0, arr.length - 1);
  }

  private static void quickSort(int[] arr, int start, int end) {
    // start가 end보다 크거나 같다면 정렬할 원소가 1개 이하이므로 정렬하지 않고 return
    if (start >= end)
      return;
    
    // 가장 왼쪽의 값을 pivot으로 지정, 실제 비교 검사는 start+1 부터 시작
    int pivot = start;
    int lo = start + 1;
    int hi = end;
    
    // lo는 현재 부분배열의 왼쪽, hi는 오른쪽을 의미
    // 서로 엇갈리게 될 경우 while문 종료
    while (lo <= hi) {
      while (lo <= end && arr[lo] <= arr[pivot]) // 피벗보다 큰 값을 만날 때까지
        lo++;
      while (hi > start && arr[hi] >= arr[pivot]) // 피벗보다 작은 값을 만날 때까지
        hi--;
      if (lo > hi)				 // 엇갈리면 피벗과 교체
        swap(arr, hi, pivot);
      else
        swap(arr, lo, hi);			 // 엇갈리지 않으면 lo, hi 값 교체 
      }
	
    // 엇갈렸을 경우, 
    // 피벗값과 hi값을 교체한 후 해당 피벗을 기준으로 앞 뒤로 배열을 분할하여 정렬 진행
    quickSort(arr, start, hi - 1);
    quickSort(arr, hi + 1, end);

  }

  private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }
}


```


<br>

## 4. 특징

- **최악의 경우 시간 복잡도 : O(n^2)**
    - 최악의 경우 pivot이 배열 내에서 가장 작은 값 또는 가장 큰 값으로 설정된다면  
      원소 n개에 대해서 n번, (n-1)번, (n-2)번...1번 의 비교가 필요하기 때문

- **평균 시간 복잡도 : O(nlogn)**
    - pivot 값이 적절히 설정된다면 그 속도가 매우 빠르다.

- **공간 복잡도 : O(nlogn)**
    - 퀵정렬은 재귀적으로 정의되므로 재귀 호출에 따른 스택이 사용된다.
    - 스택의 깊이는 n개의 원소에 대해 logn에 비례하기 때문
      
- 따라서 **in-place** 정렬이라고 하기 힘들지만,  
  실용적으로는 상대적으로 작은 메모리만을 사용하므로 흔히 in-place 정렬이라고 기술하기도 한다. 
      
- 퀵 정렬은 중복된 키값이 순서 유지될 수 있어 **not-stable**하다.

|최선의 시간복잡도|최악의 시간복잡도|
|----|----|
|![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/f45f0b72-5614-41ae-8622-148989b48295)|![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/4a3c7268-f591-42dd-b686-d784d85b1353)|


<br>


## 5. 장점과 단점

#### 장점
- 속도가 빠르다
- 시간 복잡도가 O(nlogn)을 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.
-  O(logn)만큼의 메모리 외에 추가 공간을 필요로 하지 않는다.


#### 단점
- 정렬된 리스트에 대해서는 퀵정렬의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다.
- 퀵정렬의 불균형 분할을 방지하기 위하여 피벗을 선택할 때  
 더욱 리스트를 균등하게 분할할 수 있는 데이터를 선택한다.  
  (예를들어 리스트 내의 몇개의 데이터 중에서 크기 순으로 중간 값을 피벗으로 선택한다.)
 



<hr>

#### 참고자료

- [퀵 정렬(Quick Sort)](https://velog.io/@cgotjh/%ED%80%B5-%EC%A0%95%EB%A0%ACQuick-Sort)
- [[알고리즘] 퀵 정렬(Quick Sort)이란?](https://code-lab1.tistory.com/23)
- [[알고리즘] 퀵 정렬 (Quick sort) - 자바 Java](https://erinh.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%ED%80%B5-%EC%A0%95%EB%A0%AC-Quick-sort-%EC%9E%90%EB%B0%94-Java)
