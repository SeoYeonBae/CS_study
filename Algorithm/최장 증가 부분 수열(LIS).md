# 📌 최장 증가 부분 수열(LIS)

아래와 같은 경우를 **'최장 증가 부분 수열'(Longest Increasing Subsequence)** 이라고 부른다

> 원소가 n개인 배열의 부분 수열 중,
> 1. 각 원소가 이전 원소보다 크고
> 2. 수열의 길이가 최대인 부분 수열
>  
>   
> ex) {6,2,5,1,7}의 부분수열에는
{2,5}, {2,7}도 있지만
{2,5,7}이 LIS가 된다


<br>


## 1. 구현 방법

### 1️⃣ DP를 이용한 방법

**(1)** 수열의 길이와 같은 dp 배열 선언  
**(2)** 수열을 **처음부터 끝까지 순서대로 1개씩 탐색**  
   　　(2-1) dp[i]를 1로 초기화  
   　　(2-2) 현재 위치 i에서 **새로 시작하는 LIS값**과, **이전에 있는 dp[j]에 dp[i]를 더한 값을** 비교한다.  
   　　(2-3) 0에서 현재 위치 i까지 탐색하며 **max값을 갱신**한다.  
**(3)** dp배열 원소 중 **가장 큰값 출력**


<br>


**📢 시간복잡도 O(n^2)**

```
dp[0] = 1;

for(int i=1; i<n; i++) {
			dp[i] = 1;
			for(int j=0; j<i; j++) {
				if(arr[i] > arr[j]) {
					dp[i] = Math.max(dp[i], dp[j]+1);
				}
			}			
		}

```



### 2️⃣ 이분탐색을 이용한 방법

주어진 배열의 인덱스를 하나씩 살펴보면서  
**그 숫자가 들어갈 위치**를 이분탐색으로 탐색해서 넣는다.

<br>

**📢 시간복잡도 O(nlog n)**


![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/2ff096e0-588d-46ee-a82e-a50923deb3dd)



```

// arr의 두번째부터 마지막까지 하나씩 LIS와 비교하면서 넣어준다.
  int j = 0;
  int i = 1;

  while (i < n) {
		// lis 배열의 맨 뒤의 값보다 arr[i]가 더 크면 그것을 lis 배열 맨 뒤에 넣어준다.
		if (lis[j] < arr[i]) {
			lis[j + 1] = arr[i];
			j += 1;
		}
		// arr[i]값이 더 작으면, arr[i]의 값이 lis 배열 중 어느 곳에 들어올지 이분탐색한다.
		else {
      // 0부터 j까지 탐색하면서 arr[i]가 들어갈 수 있는 위치를 찾아서 idx에 반환
			int idx = binarysearch(0, j, arr[i]);
			lis[idx] = arr[i];
		}
		i += 1;
	}


// LIS를 유지하기 위해 숫자가 들어갈 위치를 이분탐색으로 찾는 함수
int binarysearch(int left, int right, int target) {

	int mid;

  // lis 배열에 들어갈 target=arr[i]의 위치를 이분탐색으로 찾기
	while (left < right) {
		mid = (left + right) / 2; // 중간값 설정

		if (lis[mid] < target) {
			left = mid + 1;
		}
		else {
			right = mid;
		}
	}
	return right;
}


```


<br>

## 2. 예제

### BOJ 2352번 : 반도체 설계

<br>

왼쪽 그림에 n개의 포트가 있고, 오른쪽 그림에 n개의 포트가 있습니다.  

왼쪽 포트와 오른쪽 포트를 어떻게 연결하는지 정보가 주어지는데, 아래와 같이 서로 꼬이면 안 됩니다.  


**서로 꼬이지 않도록 하면서, 최대 몇 개의 포트를 서로 연결할 수 있는지** 알아내야 합니다.  

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/5ba81f06-69f9-46e4-957f-e83bb83282c3)


<br>

- **Input**

첫 줄에 정수(1<=n<=40,000)가 주어진 후   
다음 줄부터 차례대로 1번 포트와 연결되는 포트, 2번 포트와 연결되는 포트, … , n번 포트와 연결되는 포트의 번호가 주어지고  
이들은 모두 1 이상 n 이하의 숫자이며 서로 같은 수는 없습니다.


- **Output**

꼬이지 않고 최대로 연결할 수 있는 개수를 출력합니다.

<br>

- **풀이 방법**


![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/fc20ac09-dc8e-4b17-866d-b19cae6b81ef)

위처럼 1,3,4 번 포트가 각각 2 - 3 - 5 와 연결되면 꼬이지 않고 연결할 수 있습니다.  

(2,3,5번 포트가 1 - 3 - 4 로 연결해도 가능)  

여기에서 알 수 있는 것은, 이 문제는 **주어진 연결정보인 2, 1, 3, 5, 4를 가지고**  
LIS(Longest Increasing Subsequence, 최장 증가 부분 수열) 문제를 푸는 것과 동일하다는 점입니다.  


그러나 **인풋이 4만개이므로, DP를 사용한 O(n^2) 알고리즘은 적합하지 않다**고 볼 수 있습니다.  
문제의 **제한시간이 2초**로 주어져 있기 때문입니다.  


따라서 O(nlog n)의 시간복잡도를 가진, **이분탐색을 결합한 LIS 알고리즘으로** 문제를 풀어야 합니다.

<br>

<hr>

#### 참고자료

- [최장 증가 부분 수열(LIS) 알고리즘](https://chanhuiseok.github.io/posts/algo-49/)
- [[Algorithm] 최장 증가 수열 (LIS)](https://simsim231.tistory.com/204)
- [[알고리즘] 가장 긴 증가하는 부분 수열 LIS ](https://loosie.tistory.com/376)
