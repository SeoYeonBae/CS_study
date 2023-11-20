# :pushpin: 계수 정렬(Counting Sort)

## :computer: 계수 정렬이란?

:heavy_check_mark: 정의

- 배열 내에 특정한 값이 몇번 등장했는지에 따라 정렬을 수행

:heavy_check_mark: 정렬 과정

1. 입력받은 배열 A의 요소값들의 등장횟수를 저장하는 배열 B와 최종적으로 정렬될 값들을 담을 배열 C를 준비
2. 입력받은 배열에서 값을 하나씩 꺼내서 해당 값을 배열 B의 index로 사용해 카운트를 증가시킴 (B[A[i]]++)
3. B가 완성되면 B의 각 요소들을 누적합으로 갱신 (B[i] += B[i-1])
4. A의 값을 하나씩 꺼내서 해당 값을 B의 index로 사용하고 참조된 B의 값을 배열 C의 index로 사용해서 배열 C에 A에서 꺼낸 값을 넣음 (C[B[A[i]]] = A[i])
5. 사용된 B의 값을 하나 감소시킴 (B[A[i]]--)
6. A의 모든 요소에 대해 4, 5번을 반복

## :computer: 계수 정렬 과정

[9, 23, 0, 12, 32, 5, 1, 23, 123, 3]과 같은 배열이 있다고 가정

1. 배열에서 각 숫자가 몇번씩 나왔는지 count해서 저장

   ![image](https://github.com/SeoYeonBae/CS_study/assets/69101568/b175a069-ec6e-4615-8b16-37ba13aa2116)

2. count 배열이 완성이 되면 이 배열을 자신 앞에 숫자가 총 몇개가 있는지 count해서 저장한 sum 배열로 갱신

   ![image](https://github.com/SeoYeonBae/CS_study/assets/69101568/f002192f-dbab-4f29-9dee-05683020eaf1)

3. 배열에서 값을 하나씩 꺼내서 sorted[sum[A[i]]]에 해당 값을 저장하고 count를 하나 감소시킴 count[A[i]]-- 이 과정을 반복한다

   ![image](https://github.com/SeoYeonBae/CS_study/assets/69101568/3a7a8ed7-2a17-46d0-b64b-d23b62dac175)

   ![image](https://github.com/SeoYeonBae/CS_study/assets/69101568/9b63bc74-4489-4e14-9a4d-2b632374524a)

## :computer: 계수 정렬 java 코드

```
int arr[5]; 		// [5, 4, 3, 2, 1]
int sorted_arr[5];
// 과정 1 - counting 배열의 사이즈를 최대값 5가 담기도록 크게 잡기
int counting[6];	// 단점 : counting 배열의 사이즈의 범위를 가능한 값의 범위만큼 크게 잡아야 하므로, 비효율적이 됨.

// 과정 2 - counting 배열의 값을 증가해주기.
for (int i = 0; i < arr.length; i++) {
    counting[arr[i]]++;
}
// 과정 3 - counting 배열을 누적합으로 만들어주기.
for (int i = 1; i < counting.length; i++) {
    counting[i] += counting[i - 1];
}
// 과정 4 - 뒤에서부터 배열을 돌면서, 해당하는 값의 인덱스에 값을 넣어주기.
for (int i = arr.length - 1; i >= 0; i--) {
    counting[arr[i]]--;
    sorted_arr[counting[arr[i]]] = arr[i];
}
```

## :computer: 장점 & 단점

:heavy_check_mark: 장점

- O(n)의 시간복잡도

:heavy_check_mark: 단점

- 배열 사이즈 n만큼 돌 때, 증가시켜주는 count 배열의 크기가 큼
- 메모리 낭비가 심함

---

<br>

참고

- [계수 정렬(Counting Sort)](https://gyoogle.dev/blog/algorithm/Counting%20Sort.html)
- [알고리즘 6일차 - O(n) 정렬, 계수 정렬](https://velog.io/@chappi/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-6%EC%9D%BC%EC%B0%A8-On-%EC%A0%95%EB%A0%AC-%EA%B3%84%EC%88%98-%EC%A0%95%EB%A0%AC)
