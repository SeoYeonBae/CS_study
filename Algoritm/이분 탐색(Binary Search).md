# 🔍 이분 탐색(Binary Search)

**정렬되어 있는 리스트**에서 **탐색 범위를 절반씩 좁혀가며** 데이터를 탐색하는 방법

<br>

## 1. 과정


#### (1) 데이터가 정렬된 상태에서 시작

#### (2) left(시작점), right(끝점) 사이에 mid(중간값)을 지정

#### (3) left, right 값을 통해 mid 탐색

　3-1) 찾고자하는 값 > mid값  : **left를 mid 뒤로** 이동

　3-2) 찾고자하는 값 < mid값  :  **right를 mid 앞으로** 이동

#### (4) 위의 과정을 left가 right 값보다 커질 때까지 반복


 ![img](https://blog.kakaocdn.net/dn/chtpWt/btryCOMXtrD/TPbK21xfTIAg8MHLd42o7k/img.gif)

<br>


## 2. 예제 코드

```
    int arr[8]  = {1,3,7,8,9,15,17,21};
    
    int target = 7;
    int left = 0;
    int right = 7;
    int mid;
    
    while(left <= right)
    {
        mid = (left+right)/2;  
        if(arr[mid] < target )
            left = mid+1;  
        else if(arr[mid] > target)
            right = mid-1;
        else
            return mid;
    }

```

<br>

## 3. 시간복잡도

이진 탐색 알고리즘은 중간 값과 찾고자하는 값의 비교가 이루어질때마다 탐색 범위가 1/2로 줄어든다.  
정렬된 데이터의 크기를 n으로, 비교 횟수를 k라고 정의하자.
  
n * (2/1)^k = 1  
n = 2^k  
k = log n  
  
즉, n크기의 데이터에 대한 이진탐색 알고리즘의 시간복잡도는 **O(log n)**

<br>

## 4. 장단점
- **장점** : 선형 탐색에 비해 빠른 탐색 시간이 (선형 탐색 = O(n))
- **단점** : 정렬된 리스트에서만 사용 가능

<br>


<hr>

#### 참고자료

- [[알고리즘] 이분 탐색 / 이진 탐색 (Binary Search)](https://velog.io/@kimdukbae/%EC%9D%B4%EB%B6%84-%ED%83%90%EC%83%89-%EC%9D%B4%EC%A7%84-%ED%83%90%EC%83%89-Binary-Search)
- [[알고리즘] 이진(이분) 탐색(Binary Search)](https://computer-science-student.tistory.com/565)
- [[ 알고리즘] 이분탐색(Binary Search)](https://tnwlswkd.tistory.com/112)
- [이진탐색](https://velog.io/@ssuda/%EC%9D%B4%EC%A7%84%ED%83%90%EC%83%89Binary-Search-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
