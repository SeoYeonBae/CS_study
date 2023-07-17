# :pushpin: 삽입 정렬(Insertion Sort)

## :computer: 삽입 정렬이란?

:heavy_check_mark: 정의

- 2번째 원소부터 시작하여 그 앞의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입하여 정렬하는 알고리즘
- 자료 배열의 모든 요소를 앞에서부터 차례대로 **이미 정렬된 배열 부분과 비교 하여, 자신의 위치를 찾아 삽입함**으로써 정렬을 완성하는 알고리즘
- 최선의 경우 O(N)이라는 엄청나게 빠른 효율성

## :computer: 삽입 정렬 과정

1. 2번째 위치의 값을 temp에 저장
2. temp와 이전에 있는 원소들과 비교하며 삽입해나감
3. 1번으로 돌아가 다음 위치의 값을 emp에 저장하고 반복

## :computer: 삽입 정렬 java 코드

```
void insertionSort(int[] arr)
{
   for(int index = 1 ; index < arr.length ; index++){ // 1.
      int temp = arr[index];
      int prev = index - 1;
      while( (prev >= 0) && (arr[prev] > temp) ) {    // 2.
         arr[prev+1] = arr[prev];
         prev--;
      }
      arr[prev + 1] = temp;                           // 3.
   }
   System.out.println(Arrays.toString(arr));
}
```

1. 첫 번째 원소 앞(왼쪽)에는 어떤 원소도 갖고 있지 않기 때문에, 두 번째 위치(index)부터 탐색을 시작한다. temp에 임시로 해당 위치(index) 값을 저장하고, prev에는 해당 위치(index)의 이전 위치(index)를 저장한다.
2. 이전 위치(index)를 가리키는 prev가 음수가 되지 않고, 이전 위치(index)의 값이 '1'번에서 선택한 값보다 크다면, 서로 값을 교환해주고 prev를 더 이전 위치(index)를 가리키도록 한다.
3. '2'번에서 반복문이 끝나고 난 뒤, prev에는 현재 temp 값보다 작은 값들 중 제일 큰 값의 위치(index) 를 가리키게 된다. 따라서, (prev+1)에 temp 값을 삽입해준다.

## :computer: 시간복잡도 & 공간복잡도

:heavy_check_mark: 시간복잡도

- 역으로 정렬되어 있을 경우가 최악의 경우이며, (n-1) + (n-2) + .... + 2 + 1 => n(n-1)/2 => O(n^2)
- 모두 정렬이 되어 있는 경우가 최선의 경우이며, 한 번씩만 비교하기 때문에 O(n)
- **최선의 경우 O(n)이고 최악의 경우 O(n^2)**

:heavy_check_mark: 공간복잡도

- 주어진 배열 안에서 swap만 하기 때문에 O(n)

## :computer: 장점 & 단점

:heavy_check_mark: 장점

- 단순한 알고리즘
- 대부분의 원소가 이미 정렬되어 있는 경우, 매우 효율적
- 정렬하고자 하는 배열 안에서만 swap하므로 추가 메모리 공간이 필요 없음
- selection이나 bubble sort보다는 상대적으로 빠름
- 안정 정렬 (정렬 전 동일한 키 값의 요소 순서가 정렬 후 유지가 됨)

:heavy_check_mark: 단점

- 평균과 최악의 시간복잡도가 O(n^2)
- bubble과 selection과 마찬가지로 배열의 길이가 길수록 비효율적

---

<br>

참고

- [삽입 정렬(Insertion Sort)](https://gyoogle.dev/blog/algorithm/Insertion%20Sort.html)
- [자바 [JAVA] - 삽입 정렬 (Insertion Sort)](https://st-lab.tistory.com/179)
- [[알고리즘] 안정 정렬 (Stable Sort)](https://riverblue.tistory.com/39)
