# :pushpin: DFS & BFS

_그래프 탐색이란? 하나의 정점으로부터 시작하여 차례대로 모든 정점들을 한 번씩 방문하는 것!_

## :computer: DFS란?

:heavy_check_mark: 정의

- 깊이 우선 탐색
- 루트 노드 (혹은 임의의 노드)에서 시작해서 다음 branch로 넘어가기 전에 해당 branch를 완벽하게 탐색하는 방법
- 한 방향으로 갈 수 있을 때까지 계~~속 가다가 더 이상 갈 수 없으면 다시 가장 가까운 갈림길로 돌아와서 다시 탐색

:heavy_check_mark: 특징

- 자기 자신을 호출하는 순환 알고리즘의 형태를 가지고 있음
- 스택 혹은 재귀함수를 통해 구현
- 모든 경로를 다 방문해야 하는 경우에 사용하기 적합하다

![Depth-First-Search](https://github.com/SeoYeonBae/CS_study/assets/69101568/139b259e-31f1-460a-903b-5f6b3b0341bf)

:heavy_check_mark: java 코드 (재귀)

```
public class Study_DFS_Recursion {

	// 방문처리에 사용 할 배열선언
	static boolean[] vistied = new boolean[9];

	// 그림예시 그래프의 연결상태를 2차원 배열로 표현
	// 인덱스가 각각의 노드번호가 될 수 있게 0번인덱스는 아무것도 없는 상태라고 생각하시면됩니다.
	static int[][] graph = {{}, {2,3,8}, {1,6,8}, {1,5}, {5,7}, {3,4,7}, {2}, {4,5}, {1,2}};

	public static void main(String[] args) {
		dfs(1);
	}

	static void dfs(int nodeIndex) {
		// 방문 처리
		vistied[nodeIndex] = true;

		// 방문 노드 출력
		System.out.print(nodeIndex + " -> ");

		// 방문한 노드에 인접한 노드 찾기
		for (int node : graph[nodeIndex]) {
			// 인접한 노드가 방문한 적이 없다면 DFS 수행
			if(!vistied[node]) {
				dfs(node);
			}
		}
	}
}
```

:heavy_check_mark: java 코드 (스택)

```
public class Study_DFS_stack {

	// 방문처리에 사용 할 배열선언
	static boolean[] vistied = new boolean[9];

	// 그림예시 그래프의 연결상태를 2차원 배열로 표현
	// 인덱스가 각각의 노드번호가 될 수 있게 0번인덱스는 아무것도 없는 상태라고 생각하시면됩니다.
	static int[][] graph = {{}, {2,3,8}, {1,6,8}, {1,5}, {5,7}, {3,4,7}, {2}, {4,5}, {1,2}};

	// DFS 사용 할 스택
	static Stack<Integer> stack = new Stack<>();

	public static void main(String[] args) {

		// 시작 노드를 스택에 넣어줍니다.
		stack.push(1);
		// 시작 노드 방문처리
		vistied[1] = true;

		// 스택이 비어있지 않으면 계속 반복
		while(!stack.isEmpty()) {

			// 스택에서 하나를 꺼냅니다.
			int nodeIndex = stack.pop();

			// 방문 노드 출력
			System.out.print(nodeIndex + " -> ");

			// 꺼낸 노드와 인접한 노드 찾기
			for (int LinkedNode : graph[nodeIndex]) {
				// 인접한 노드를 방문하지 않았을 경우에 스택에 넣고 방문처리
				if(!vistied[LinkedNode]) {
					stack.push(LinkedNode);
					vistied[LinkedNode] = true;
				}
			}
		}
	}
}
```

## :computer: BFS란?

:heavy_check_mark: 정의

- 너비 우선 탐색
- 루트 노드 (혹은 임의의 노드)에서 시작해서 인접한 노드를 먼저 탐색하는 방법
- 시작 정점으로부터 가까운 정점들을 모두 먼저 방문하고 멀리 떨어져 있는 정점을 나중에 방문

:heavy_check_mark: 특징

- 노드 사이의 최단 경로를 찾고 싶을 때 사용
- 먼저 방문한 노드들을 차례로 꺼낼 수 있는 자료구조인 **큐**를 사용

![Breadth-First-Search-Algorithm](https://github.com/SeoYeonBae/CS_study/assets/69101568/27d53853-d46b-417e-a5b7-2ed721b72a8d)

:heavy_check_mark: java 코드

```
public class StudyBFS {

	public static void main(String[] args) {

		// 그래프를 2차원 배열로 표현해줍니다.
		// 배열의 인덱스를 노드와 매칭시켜서 사용하기 위해 인덱스 0은 아무것도 저장하지 않습니다.
		// 1번인덱스는 1번노드를 뜻하고 노드의 배열의 값은 연결된 노드들입니다.
		int[][] graph = {{}, {2,3,8}, {1,6,8}, {1,5}, {5,7}, {3,4,7}, {2}, {4,5}, {1,2}};

		// 방문처리를 위한 boolean배열 선언
		boolean[] visited = new boolean[9];

		System.out.println(bfs(1, graph, visited));
		//출력 내용 : 1 -> 2 -> 3 -> 8 -> 6 -> 5 -> 4 -> 7 ->
	}

	static String bfs(int start, int[][] graph, boolean[] visited) {
		// 탐색 순서를 출력하기 위한 용도
		StringBuilder sb = new StringBuilder();
		// BFS에 사용할 큐를 생성해줍니다.
		Queue<Integer> q = new LinkedList<Integer>();

		// 큐에 BFS를 시작 할 노드 번호를 넣어줍니다.
		q.offer(start);

		// 시작노드 방문처리
		visited[start] = true;

		// 큐가 빌 때까지 반복
		while(!q.isEmpty()) {
			int nodeIndex = q.poll();
			sb.append(nodeIndex + " -> ");
			//큐에서 꺼낸 노드와 연결된 노드들 체크
			for(int i=0; i<graph[nodeIndex].length; i++) {
				int temp = graph[nodeIndex][i];
				// 방문하지 않았으면 방문처리 후 큐에 넣기
				if(!visited[temp]) {
					visited[temp] = true;
					q.offer(temp);
				}
			}
		}
		// 탐색순서 리턴
		return sb.toString() ;
	}
}
```

## :computer: DFS와 BFS의 시간복잡도

- 인접 행렬의 경우 O(V^2)
- 인접 리스트의 경우 O(V+E)
- 그래서 정점에 비해 간선의 수가 적은 **희소 그래프**일 경우 인접리스트로 구현하는 것이 훨씬 유리함

---

<br>

참고

- [DFS & BFS](https://gyoogle.dev/blog/algorithm/DFS%20&%20BFS.html)
- [[알고리즘] 깊이 우선 탐색(DFS)이란](https://gmlwjd9405.github.io/2018/08/14/algorithm-dfs.html)
- [[알고리즘] 너비 우선 탐색(BFS)이란](https://gmlwjd9405.github.io/2018/08/15/algorithm-bfs.html)
- [[Algorithm] DFS (Depth-first Search)를 Java로 구현해보자!](https://codingnojam.tistory.com/44)
- [[Algorithm] BFS(Breadth-first search)를 Java로 구현해보자!](https://codingnojam.tistory.com/41)
