# π νΈλ¦¬
### 1. κ°λ

- κ°μ κ°μ§ Nodeμ μ΄ λΈλλ€μ μ°κ²°ν΄μ£Όλ Edgeλ‘ μ΄λ£¨μ΄μ§ μλ£κ΅¬μ‘°
- νλμ λ£¨νΈ λΈλ
- λͺ¨λ  λΈλλ€μ 0κ° μ΄μμ μμ λΈλλ₯Ό κ°μ§κ³  μμΌλ©° λ³΄ν΅ λΆλͺ¨-μμ κ΄κ³λ‘ λΆλ₯Έλ€

---

### 2. νΉμ§

- **μ¬μ΄ν΄**μ΄ μ‘΄μ¬νμ§ μλ νλμ μ°κ²° κ·Έλν (μ¬μ΄ν΄ μμΌλ©΄ κ·Έλν)
- λͺ¨λ  λΈλλ μλ£νμΌλ‘ ννμ΄ κ°λ₯
- λ£¨νΈμμ ν λΈλλ‘ κ°λ κ²½λ‘λ μ μΌνλ€
- λΈλμ κ°μκ° Nκ°λ©΄, κ°μ μ N-1κ°λ₯Ό κ°μ§λ€

---

### 3. νΈλ¦¬ μν λ°©μ

4κ°μ§
![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d532a1a4-892d-4c9b-a61f-0037361e0eba/Untitled.png](https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png)
- μ μ μν(pre-order)
    - κ° λ£¨νΈ(Root)λ₯Ό μμ°¨μ μΌλ‘ λ¨Όμ  λ°©λ¬Ένλ λ°©μ
    - (Root β μΌμͺ½ μμ β μ€λ₯Έμͺ½ μμ)
    - 1β2β4β8β9β5β10β11β3β6β13β7β14
- μ€μ μν(in-order)
    - μΌμͺ½ νμ νΈλ¦¬λ₯Ό λ°©λ¬Έ ν λ£¨νΈλ₯Ό λ°©λ¬Ένλ λ°©μ
    - (μΌμͺ½ μμ β Root β μ€λ₯Έμͺ½ μμ)
    - 8β4β9β2β10β5β11β1β6β13β3β14β7
- νμ μν(post-order)
    - μΌμͺ½ νμ νΈλ¦¬λΆν° μ€λ₯Έμͺ½ νμ νΈλ¦¬κΉμ§ λͺ¨λ  νμ νΈλ¦¬ λ°©λ¬Έ ν λ£¨νΈ λ°©λ¬Ένλ λ°©μ
    - (μΌμͺ½ μμ β μ€λ₯Έμͺ½ μμ β Root)
    - 8β9β4β10β11β5β2β13β6β14β7β3β1
- λ λ²¨ μν(level-order)
    - λ£¨νΈλΆν° κ³μΈ΅ λ³λ‘ λ°©λ¬Ένλ λ°©μ
    - 1β2β3β4β5β6β7β8β9β10β11β13β14

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

### μ°Έκ³ 

- [https://gyoogle.dev/blog/computer-science/data-structure/Tree.html](https://gyoogle.dev/blog/computer-science/data-structure/Tree.html)
- [https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)
