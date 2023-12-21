# :pushpin: 기수 정렬(Radix Sort)

## :computer: 기수 정렬이란?

:heavy_check_mark: 정의

- 데이터를 구성하는 기본 요소(Radix)를 이용하여 정렬을 진행하는 방식
- 입력 데이터의 최댓값만큼의 배열을 만들어서 정렬하는 Counting Sort의 비효율성을 개선하기 위해 사용!
- **낮은 자릿수부터 비교하여 정렬해 간다는 것을 기본 개념으로 하는 정렬 알고리즘**

:heavy_check_mark: 종류

- 가장 작은 자릿수부터 비교하는 방법 -> LSD(Least-Significant-Digit)
- 가장 큰 자릿수부터 비교하는 방법 -> MSD(Most-Significant-Digit)

:heavy_check_mark: 시간복잡도

- O(r\*n) : r은 숫자의 자릿수, n은 정렬될 수의 개수

## :computer: 기수 정렬 과정

_LSD 기준으로 설명!_

[153, 262, 37, 598, 433, 855]과 같은 배열이 있다고 가정

- 가장 큰 숫자는 855, 자리수는 3
- 가장 작은 자릿수부터 가장 큰 자릿수까지 카운팅 소트를 진행

1. 1의 자리수를 기준으로 정렬합니다
   </br>
   [262], [153], [433], [855], [037], [598]

2. 10의 자리수를 기준으로 정렬합니다. 이때, 1,2,5와 같이 10의 자리가 없는 건 10의 자리수가 0이라고 생각하면 됩니다~
   </br>
   [433, 037], [153, 855], [262], [598]

3. 100의 자리수를 기준으로 정렬합니다
   </br>
   [037], [153], [262], [433], [598], [855]

![image](https://github.com/SeoYeonBae/CS_study/assets/69101568/343ca095-0799-40bc-b2c8-e7ff07e4c1bc)

## :computer: 기수 정렬 java 코드

```
public class Main {

	static final int bucketSize = 10;

	public static void main(String[] args) {
		int[] arr = {28, 93, 39, 81, 62, 72, 38, 26};

		radix_Sort(arr.length, arr);

		for (int i = 0; i < arr.length; ++i) {
			System.out.print(arr[i] + " ");
		}
	}

	public static void radix_Sort(int n, int[] arr) {
		//bucket 초기화
		Queue<Integer>[] bucket = new LinkedList[bucketSize];
		for (int i = 0; i < bucketSize; ++i) {
			bucket[i] = new LinkedList<>();
		}

		int factor = 1;

		//정렬할 자릿수의 크기 만큼 반복한다.
		for (int d = 0; d < 2; ++d) {
			for (int i = 0; i < n; ++i) {
				bucket[(arr[i] / factor) % 10].add(arr[i]);
			}

			for (int i = 0, j = 0; i < bucketSize; ++i) {
				while (!bucket[i].isEmpty()) {
					arr[j++] = bucket[i].poll();
				}
			}

			factor *= 10;
		}
	}
}
```

## :computer: 장점 & 단점

:heavy_check_mark: 장점

- O(n)의 시간복잡도

:heavy_check_mark: 단점

- 추가적으로 버킷을 사용하기 때문에 데이터 크기에 비례한 메모리가 필요하다

---

<br>

참고

- [기수 정렬(Radix sort)](https://gyoogle.dev/blog/algorithm/Radix%20Sort.html)
- [[정렬] 7. 한 살도 이해하는 기수 정렬(radix sort)](https://10000cow.tistory.com/entry/%EC%A0%95%EB%A0%AC-7-%EA%B8%B0%EC%88%98-%EC%A0%95%EB%A0%ACradix-sort) -[기수 정렬(Radix Sort)](https://sorjfkrh5078.tistory.com/21)
- [[알고리즘] 기수 정렬(Radix Sort)](https://hongcoding.tistory.com/187)
