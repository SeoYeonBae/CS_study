## 힙 정렬(Heap Sort) 

### ❔ 힙(Heap)이란?
- *완전 이진 트리*의 일종으로, 우선순위 큐를 위하여 만들어진 자료구조           
   - *이진 트리로서 맨 아래 층을 제외하고는 완전히 채워져 있고 맨 아래층은 왼쪽부터 꽉 채워져있는 형태*
- 최댓값, 최솟값을 쉽게 추출할 수 있는 자료구조

### 📊 힙 정렬(Heap Sort)
- 최대 힙 트리나 최소 힙 트리를 구성하여 정렬하는 방법
  - 내림차순 정렬을 위해서는 최대 힙, 오름차순 정렬을 위해서는 최소 힙을 구성하면 된다
  - 최대 힙 : 부모 노드가 자식 노드보다 큰 트리

### 💻 구현
- 힙은 완전 이진 트리, 즉 꽉 찬 이진 트리이기에 배열로 구현할 수 있다.
- 부모 자식 관계를 배열의 인덱스를 사용하여 구현한다.

1. 리프가 아닌 노드 중 맨 마지막 노드부터 시작하여 부모자식의 크기가 힙 성질에 만족하는지 확인한다.
2. 부모자식의 크기가 힙 성질을 만족하지 않는 경우 만족하지 않는 두 원소를 교환
   a. 교환한 원소의 부모자식의 크기가 힙 성질에 만족하는지 확인한다. (재귀 반복)
   b. 힙 성질 만족하는 경우를 만나면 중단한다.
3. 최대 힙의 경우 루트에 있는 값이 가장 큰 값이기에 배열의 첫번째에 위치한 이 값을 배열의 맨 오른쪽 원소와 교환한다.
4. 베열의 맨 오른쪽 원소를 제외하고 다시 힙 상태로 만든 뒤 3의 과정을 반복한다.

```java
   public static void heapSort(int[] arr, int n) {

      //   힙 만들기
		for (int i = (n - 1) / 2; i >= 0; i--)
			heapify(arr, i, n - 1);

      //   정렬
		for (int i = n - 1; i > 0; i--) {
			swap(arr, 0, i);
			heapify(arr, 0, i - 1);
		}
	}

	public static void heapify(int[] arr, int left, int right) {

		int root = arr[left]; // 루트 노드
		int parent; // 부모 노드 인덱스
		int child; // 자식 노드 인덱스

		for (parent = left; parent < (right + 1) / 2; parent = child) {

			int cl = parent * 2 + 1; // 왼쪽 자식 노드 인덱스
			int cr = cl + 1; // 오른쪽 자식 노드 인덱스

			child = (cr <= right && arr[cl] < arr[cr]) ? cr : cl;

			if (root > arr[child])
				break;

			arr[parent] = arr[child];
		}
		arr[parent] = root;

	}
```
### ⌚ 시간 복잡도
1. 힙 만들기 (heapify)
  - 힙의 높이에 비례하는 시간이 소요된다.
  - 힙의 높이가 h라면 `O(h)`시간
2. 정렬
- 이진 트리로 최대/최소 힙을 만들기 위하여 재구성하는 과정이 트리의 깊이만큼 이루어지므로 `O(logn)`
- 위의 과정을 n - 1번 순환, (n - 1) * O(logn) + O(h)
- 힙 정렬의 총 수행 시간은 **`O(nlogn)`**

### 특징
- 정렬을 위한 추가적인 메모리가 필요하지 않다.
- 최선, 평균, 최악의 경우 모두 heapify 과정이 필요하기 때문에 `O(nlogn)`을 보장한다.
- 데이터 순서를 보장하지 못하는, 데이터의 순서가 바뀌는 불안정(unstable) 정렬이다.
- 데이터의 상태에 따라 다른 정렬법에 비해 느린 편이다.

### 참고
- [[알고리즘] 힙 정렬(Heap Sort)](https://hongcoding.tistory.com/186)
- [힙 정렬(Heap Sort)](https://lotuslee.tistory.com/40)
