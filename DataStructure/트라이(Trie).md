# Trie

**트라이(Trie)**란 문자열을 효율적으로 저장하고 탐색하기 위한 트리 형태의 자료 구조

![트라이(Trie) 구조 ](Trie%20c2ee07dd7ab5448aab004ce4bee1efb2/Untitled.png)

트라이(Trie) 구조 

### 시간 복잡도

원하는 값을 탐색하기 위해 자주 사용되는 이진 검색 트리의 시간 복잡도는 **O(logN)**

*하지만*

문자열의 경우 두 문자열을 비교하기 위해 문자열의 길이만큼의 시간이 걸리기에 **O(MlogN)**로 증가

이러한 단점을 해결하기 위해 문자열 탐색 자료구조 **Trie**가 등장

문자열의 길이만큼 노드를 따라가거나 추가하면 되기에 추가와 탐색 모두 **O(M)**

하지만 **공간 복잡도가 높다**는 단점이 존재한다.

알파벳을 저장하는 형태라면 a부터 z까지 26개의 공간이 필요하다는 점이다.

시간, 공간 복잡도를 고려하여 Trie 구조를 적절히 변형하여야 하는데

이러한 공간 복잡도를 낮추기 위해 **Map**을 사용한다.

### 트라이 기본 구조

- Trie는 자식 노드를 Map, 즉 <key,value> 형태로 지니고 있다.
    - key : 알파벳
    - value : key에 해당하는 자식 노드
- 루트 노드는 특정 알파벳을 의미하지 않고 자식 노드만을 지닌다.
- 루트 노드를 제외한 노드의 자손들은 공통 접두어를 지닌다.

### 구현

```jsx
public class TrieNode{

	// 자식 노드 맵
	private Map<Character, TrieNode> childNodes = new HashMap<>();

	// 마지막 글자인지 여부
	private boolean isLast;

	// 각 변수의 getter, setter

}
```

```jsx
public class Trie{

	// 루트 노드
	private TrieNode rootNode;
	
	// 생성자
	Trie() {
		rootNode = new TrieNode();
	}

	// 추가
	void insert(String word){
		TrieNode thisNode = this.rootNode;

		// 공통 접두어 이후부터 생성 (해당 계층 문자의 자식노드가 존재하지 않을 경우에만 자식 노드 생성)
		// computeIfAbsent(key, function) : function 함수는 key값이 존재하지 않을 때만 실행
		for (int i = 0; i < word.length(); i++) {
			thisNode = thisNode.getChildNodes().computeIfAbsent(word.charAt(i), c -> new TrieNode());
		}

		thisNode.setIsLast(true); // 마지막 글자 체크해주기
	} 

	// 존재 여부 확인
	boolean isContain(String word) {
		TrieNode thisNode = this.rootNode;
	
		for (int i = 0; i < word.length(); i++) {
			char character = word.charAt(i);
			TrieNode node = thisNode.getChildNodes().get(character);
	
			if (node == null)
				return false;
	
			thisNode = node;
		} // 루트 노드부터 순서대로 문자가 일치하는 자식 노드들이 존재
	
		return thisNode.isLast(); // 해당 단어의 마지막 문자에 해당하는 노드가 true일 경우 해당 단어 존재
	}

	// 삭제
	/* 
		 노드들이 부모 노드의 정보를 가지고 있지 않기 때문에
		 하위 노드로 내려가며 삭제할 단어를 탐색하고 다시 되돌아 올라오며 삭제하는 콜백 형식
		
		 삭제 조건
			1. 삭제하려는 단어는 자식 노드를 지니고 있지 않아야 한다.
			  - 삭제하려는 단어를 접두어로 지닌 단어 또한 삭제되기 때문
			2. 삭제하려는 단어의 마지막 노드 즉, 탐색이 끝나고 삭제를 시작할 첫 노드의 isLast는 true여야 한다.
			3. 삭제를 진행하며 지나치는 노드의 isLast는 false여야 한다.
				- 삭제 진행 중 isLast가 true이면 Trie에 존재하는 또다른 단어를 포함하고 있다는 의미
	*/
	void delete(String word) {
		delete(this.rootNode, word, 0); // 최초로 delete 던지는 부분
	}
	
	private boolean delete(TrieNode thisNode, String word, int index) {
			
		if (index == word.length()) { // 탐색해오면서 isLast() == true인 단어 발견 X
        if (!thisNode.isLast()) { // 삭제 조건 2번 위배
            return false;
        }
        thisNode.setIsLast(false);
        return thisNode.getChildNodes().isEmpty();
    }

    char ch = word.charAt(index);
    TrieNode node = thisNode.getChildNodes().get(ch);
    if (node == null) {
        return false;
    }
    boolean shouldDeleteCurrentNode = delete(node, word, index + 1) && !node.isLast();
		
    if (shouldDeleteCurrentNode) {
        thisNode.getChildNodes().remove(ch);
        return thisNode.getChildNodes().isEmpty();
    }
    return false;
		
	}
}
```

출처 : 

[https://www.baeldung.com/trie-java](https://www.baeldung.com/trie-java)

[https://the-dev.tistory.com/3](https://the-dev.tistory.com/3)