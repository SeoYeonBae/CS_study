# 📌 크루스칼(Kruskal)

## ✨ 1. 크루스칼 알고리즘이란?

- 그래프 내의 모든 정점들을 가장 적은 비용으로 연결하기 위해 사용되는 알고리즘
- 그래프에는 정점과 간선이 있고 간선에는 가중치가 포함되어 있음
- 그래프 내의 모든 정점을 포함하면서 사이클이 없는 연결선을 그렸을 때 가중치의 합이 최소가 되는 상황을 구해야된다? 이때 사용하는 것!
- 즉, 최소 신장 트리를 구하기 위한 알고리즘

### ✋ 여기서 잠깐! 신장 트리 vs 최소 신장 트리

||신장 트리|최소 신장 트리|
|-|-|-|
|정의|그래프의 모든 정점을 포함하면서 싸이클이없는 그래프|신장 트리 중 가중치의 합이 최소인 트리|
|개수|여러개 존재할 수 있음|한개|
|예시|![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/e85f348d-cfb3-4a04-819c-ad6da560f2b5)|![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/2393fe2e-0e54-449a-800a-a0bdcfe4236c)|


## ✨ 2. 크루스칼 알고리즘의 과정

- 그리디 알고리즘의 일종
- 즉, 간선의 가중치를 오름차순으로 정렬한 뒤 사이클을 형성하지 않는 선에서 정렬된 순서로 간선을 선택
- 사이클 판단 여부는 Union & Find 사용

### 0. 그래프 준비

![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/fe0de677-38bd-416f-83a6-119002642e53)

- 1번~4번 노드는 초기에 각각 서로소 집합 {1}, {2}, {3}, {4}로 표현
- 즉, 부모가 자기 자신이라는 뜻
- 집합 내에서 제일 작은 숫자가 그 집합에서의 루트 노드(root node) 가 되게끔 가정
- 서로 부모가 다른지 (= 사이클이 생기지 않는지) 확인하고 다르다면 Union 연산으로 합할 예정

### 1. 그래프 간선을 가중치 오름차순으로 정렬

![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/fe0de677-38bd-416f-83a6-119002642e53)
![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/06a3a83a-c289-40a1-ab6d-91719b071f13)

### 2. 1-2 선택

![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/bae0c795-50c1-461c-a541-a10b18b83596)
![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/2b0bb073-b2bc-4e7a-bddc-3af070ae67a4)

- 1과 2는 부모가 각각 다른 값이므로 사이클이 생기지 않음
- Union 연산에 의해서 같은 집합으로 합지고 2번의 부모가 1이 됨

### 3. 1-4 선택

![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/c3372074-929c-4a79-aba8-ef8e1ceac4ba)
![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/d45dab6a-0188-4236-9c93-f1c745270699)

- 1과 4는 부모가 서로 다름!
- 따라서, Union 연산으로 합칠 수 있음

### 4. 2-4 선택

![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/c1bf79d1-a6af-4987-8f71-569646448424)
![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/81651fce-0c60-4800-9f01-475ad127fa66)

- 2와 4는 이미 부모가 1로 같음
- 서로 부모가 같기 때문에 Union 연산을 하지 않음
- Union 연산 실행 시 위 그림처럼 사이클을 형성하게 

### 5. 2-3 선택

![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/2cae7e61-c681-42c1-b967-36040ac9530d)
![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/80beecbe-266e-4af3-aaf6-07aba4bbbefb)

- 모든 정점이 연결되었기 때문에 종료

## ✨ 3. 코드로 보는 크루스칼

```
public class KruskalTest {

  // 출발 정점, 도착 정점, 두 정점 사이의 가중치를 포함하는 자료구조 Edge 선언
	static class Edge implements Comparable<Edge>{
		int from, to, weight;

		public Edge(int from, int to, int weight) {
			super();
			this.from = from;
			this.to = to;
			this.weight = weight;
		}
		
		@Override
		public int compareTo(Edge o) {
    // 비용이 양수와 음수 섞여있다면 비교할 때 compare 사용
    // return Integer.compare(this.weight, o.weight);	
			return this.weight - o.weight;
		}
	}
	
	static int[] parents;
	static int V, E;
	static Edge[] edgeList;

  // 크기가 1인 서로소 집합 생성
	static void make() {	
		parents = new int[V];
    // 모든 노드가 자신을 부모로 하는 (대표자) 집합으로 만듦
		for (int i = 0; i < V; i++) {	
			parents[i] = i;
		}
	}


	// a의 부모 찾기
	static int find(int a) {	
		if(parents[a] == a) return a;
		return parents[a] = find(parents[a]);
	}
	
	// 리턴값 : true ==> union 성공
	static boolean union(int a, int b) {
		int aRoot = find(a);
		int bRoot = find(b);
		
    // 이미 부모가 같음 = 싸이클 생김
		if(aRoot == bRoot) return false;
		
		parents[bRoot] = aRoot;
		return true;
	}
	
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine(), " ");
		V = Integer.parseInt(st.nextToken());  // 정점의 수
		E = Integer.parseInt(st.nextToken());  // 간선의 수
		
		edgeList = new Edge[E];
		
		for (int i = 0; i < E; i++) {
			st = new StringTokenizer(br.readLine(), " ");
			edgeList[i] = new Edge(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()));
		}
		
		make();
    // 간선의 가중치를 오름차순 정렬
		Arrays.sort(edgeList);
		
		int result = 0;
		int count = 0;
		for(Edge edge : edgeList) {
			if(union(edge.from, edge.to)) {
				result += edge.weight;
        // (정점의 수 - 1)개만큼 연결했다면 멈춤
				if(++count == V-1) break;
			}
		}

    // 가중치의 최소합 출력
		System.out.println(result);
	}
}
```

## ✨ 4. 시간복잡도

- 간선의 개수가 E개일 때 O(ElogE)의 시간복잡도를 가짐
- 가장 많은 시간을 요구하는 곳은 간선의 정렬을 수행하는 부분
- 표준 라이브러리를 이용해 E개의 데이터를 정렬하기 위한 시간복잡도가 O(ElogE)

---

##### 참고

- [크루스칼 알고리즘(Kruskal Algorithm), 최소 신장 트리(MST)](https://chanhuiseok.github.io/posts/algo-33/)
- [크루스칼 알고리즘(Kruskal Algorithm](https://m.blog.naver.com/ndb796/221230994142)
