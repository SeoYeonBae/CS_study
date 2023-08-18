# 📌 Array & ArrayList & LinkedList

## 1. Array

- 연관된 데이터가 **연속된 메모리 공간**에 **순차적**으로 저장된다.

- 메모리 할당 후 더이상 증감할 수 없다.

![image](https://user-images.githubusercontent.com/63834758/199028769-5e604601-3622-47aa-83c8-c5635fc0bd2c.png)

<br>
<br>

## 2. Array List

- 데이터가 **연속적으로** 늘어선 배열의 형식
- Array와 다르게 메모리 할당 후 **증감할 수 있다.** ( 속도 지연 가능성 )

- Array와 같이 index를 가지므로 **데이터 접근 속도가 빠르다.**
- 처음 또는 마지막이 아닌 중간에 삽입 & 삭제할 경우 **O(N)**
<br>

![image](https://user-images.githubusercontent.com/63834758/204771848-f3e300e3-453a-4f72-89bf-4e1fb0179221.png)

<br>
<br>

## 3. Linked List

- **자료의 주소 값으로** 서로 연결되어 있는 구조
- 자료(Node)들을 저장 공간에 **불연속적인 단위로 저장**한다.

- ArrayList와 마찬가지로 **메모리 추가 할당이 가능하다.**

- 연결(pointer)를 위한 별도의 데이터 공간이 필요하므로 저장 공간이 낭비된다.

![image](https://user-images.githubusercontent.com/63834758/200721995-bb9f59d4-aeaf-4134-ad72-f48e4364f037.png)
<br>
<br>

## 4. 정리

| 기준          | Array         | ArrayList | LinkedList         |
| :-------------: | :-------------: | :---------: | :------------------: |
| **검색 속도**     | 빠름 (무작위 접근 가능) | 빠름      | 느림 (순차 접근)        |
| **삽입 및 삭제**  | O(n)          | O(n)    | O(n)             |
| **저장공간 낭비** | 중간 (null)   | 낮음      | 높음 (포인터 사용) |

<br>
<br>

- 정적인 데이터 활용하고
    - 삽입, 삭제가 드문 경우 : Array
    - 조회가 더 빈번한 경우 : Array List

- 동적인 데이터 활용하고
    - 삽입, 삭제가 빈번한 경우 : Linked List
    - 조회가 더 빈번한 경우 : Array List

<br>
<br>
<hr>

### 참고

- [Linked List vs Array List](https://www.nextree.co.kr/p6506/)

- [Array vs ArrayList vs LinkedList](https://gwang920.github.io/datastructure/Array-ArrayList-LinkedList-%EB%B3%B5%EC%82%AC%EB%B3%B8/)

- [[자료구조] 배열 Array, 배열 리스트 ArrayList, 연결 리스트 LinkedList](https://velog.io/@nnnyeong/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EB%B0%B0%EC%97%B4-Array-%EB%B0%B0%EC%97%B4-%EB%A6%AC%EC%8A%A4%ED%8A%B8-ArrayList-%EC%97%B0%EA%B2%B0-%EB%A6%AC%EC%8A%A4%ED%8A%B8-LinkedList)
