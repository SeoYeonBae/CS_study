# 📌 트리
### 1. 개요

- 값을 가진 Node와 이 노드들을 연결해주는 Edge로 이루어진 자료구조
- 루트 노드
- 모든 노드들은 0개 이상의 자식 노드를 가지고 있으며 보통 부모-자식 관계로 부른다

---

### 2. 특징

- **사이클**이 존재하지 않음 (사이클 있으면 그래프)
- 모든 노드는 자료형으로 표현이 가능
- 루트에서 한 노드로 가는 경로는 유일하다
- 노드의 개수가 N개면, 간선은 N-1개를 가진다

---

### 3. 트리 순회 방식

4가지
![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d532a1a4-892d-4c9b-a61f-0037361e0eba/Untitled.png](https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png)
- 전위 순회(pre-order)
    - 각 루트(Root)를 순차적으로 먼저 방문하는 방식
    - (Root → 왼쪽 자식 → 오른쪽 자식)
    - 1→2→4→8→9→5→10→11→3→6→13→7→14
- 중위 순회(in-order)
    - 왼쪽 하위 트리를 방문 후 루트를 방문하는 방식
    - (왼쪽 자식 → Root → 오른쪽 자식)
    - 8→4→9→2→10→5→11→1→6→13→3→14→7
- 후위 순회(post-order)
    - 왼쪽 하위 트리부터 오른쪽 하위 트리까지 모든 하위 트리 방문 후 루트 방문하는 방식
    - (왼쪽 자식 → 오른쪽 자식 → Root)
    - 8→9→4→10→11→5→2→13→6→14→7→3→1
- 레벨 순회(level-order)
    - 루트부터 계층 별로 방문하는 방식
    - 1→2→3→4→5→6→7→8→9→10→11→13→14

### **Code**

```java
public class Tree<T> {
    private Node<T> root;

    public Tree(T rootData) {
        root = new Node<T>();
        root.data = rootData;
        root.children = new ArrayList<Node<T>>();
    }

    public static class Node<T> {
        private T data;
        private Node<T> parent;
        private List<Node<T>> children;
    }
}
```

---

### 참고

- [https://gyoogle.dev/blog/computer-science/data-structure/Tree.html](https://gyoogle.dev/blog/computer-science/data-structure/Tree.html)
