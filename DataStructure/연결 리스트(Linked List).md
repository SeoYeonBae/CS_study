# 📌 연결 리스트(Linked List)

## 1. 개념

- **Node**를 이용해 자료의 주소 값으로 서로 연결되어 있는 구조
- 트리의 근간이 되는 자료구조이다.

<br><br>

![image](https://user-images.githubusercontent.com/63834758/200341034-6cb3d7f4-a0c0-4481-b348-a4865b6ffc32.png)

<br>

- **Node** : 데이터 저장 단위 ( Data + Pointer )
- **Pointer** : 다음에 연결된 node의 주소 정보를 갖고 있다.
- **Head**
- **Tail**

<br>
<br>

## 2. 특징

- 자료(Node)들을 저장 공간에 **불연속적인** 단위로 저장한다.
- 배열과 다르게 데이터 공간을 미리 할당하지 않아도 된다.
- 연결(pointer)를 위한 **별도의 데이터 공간**이 필요하므로 저장 공간 효율이 높지 않다.


<br>
<br>

## 3. 삽입과 삭제

### (1) 삽입

![image](https://user-images.githubusercontent.com/63834758/200341849-0e551a78-215a-4b47-b892-ef0293e792e9.png)

<br>

- 삽입할 위치를 찾는다
- 새로운 Node의 주소 값을 Node pointer로 연결해준다.
- 새로운 Node의 pointer를 그 다음 Node의 주소값에 연결한다.

<br><br>

### (2) 삭제

![image](https://user-images.githubusercontent.com/63834758/200342636-c7652a4a-779e-4fb7-b726-23ba428856f0.png)

- **head 삭제** :  head의 다음 Node가 head가 되도록 변경한다.
- **tail 삭제** : tail 앞에 있는 Node의 주소값을 null로 변경한다.
- **중간 Node 삭제** : Node의 pointer를 Node.next에서 Node.next.next로 바꾸어 연결해주고 Node.next를 삭제한다.
 
<br>
<br>

## 4. 시간복잡도

- **검색, 삽입, 삭제** 모두 해당 Node를 찾아가기 위해 모든 요소를 **sequential access(순차접근)** 해야 하므로 O(n)
- 다만 처음과 끝에만 삽입, 삭제를 진행하는 경우에는 O(1)

<br>
<br>

### 5. 이외의 다양한 Linked List

![image](https://user-images.githubusercontent.com/63834758/200342729-6fded566-8156-45df-b597-648fc47ed5a6.png)


- 이중 연결 리스트 : Node의 pointer가 이전 Node, 다음 Node를 모두 가리키고 있다. (양방향 연결)
- 원형 연결 리스트
- 다중 연결 리스트

<hr>

참고

- https://opentutorials.org/module/1335/8821
- https://www.nextree.co.kr/p6506/
- https://velog.io/@keemtj/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EB%A7%81%ED%81%AC%EB%93%9C-%EB%A6%AC%EC%8A%A4%ED%8A%B8Linked-List
