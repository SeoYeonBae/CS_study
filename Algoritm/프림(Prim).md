## 프림(Prim)


#### 최소 신장 트리 (MST)
- *Minimum Spanning Tree*
- 무향 연결 그래프 ( 모든 정점 간에 경로가 존재하는 그래프 )
- 간선들이 가중치를 갖는 그래프에서 간선 가중치의 합이 가장 작은 트리

### 개념
- 최소 신장 트리를 찾는 알고리즘 중 하나
- Greedy 알고리즘의 일종으로 최적해를 보장하는 드문 예
- 정점을 추가하면서 모든 정점을 포함할 때까지 하나의 트리(집합)을 확장시켜가는 방식

### 흐름

#### 1️⃣ 임의의 정점을 선택하여 비어있는 집합 S에 포함시킨다.         
- 임의의 시작점 D 선택
#### 2️⃣ S에 있는 노드와 S에 없는 연결된 노드 사이의 간선 중 가중치가 최소인 간선을 찾는다. (사이클 형성하지 않는 간선)  
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/4dd58c07-2cfb-4f60-b066-22364620cc26)                           

#### 3️⃣ 찾은 간선이 연결하는 두 노드 중, S에 없는 노드를 S에 포함시킨다.     
- A를 집합 S에 포함시킨다.
#### 4️⃣ 모든 정점이 S에 포함될 때까지 2️⃣, 3️⃣ 과정을 반복한다.  
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/99cfb366-3257-490e-af6c-1cda8d843897)



#### 🔄 이완 (Relaxation)
![image](https://github.com/SeoYeonBae/CS_study/assets/63505110/d3fb8c43-8a39-4676-84fe-6039ba8775cf)                 
- (f)에서 (g)로 넘어가는 과정에서 12의 값이 7로 바뀌었는데 이렇게 값이 바뀌는 것을 이완(Relaxation)이라 한다.

### 구현
 ``` java
  public static class Edge implements Comparable<Edge>{
	int v; // 진입하는 정점
	int w; // 가중치
	Edge(int vertex, int weight) {
		this.v = vertex;
		this.w = weigth;
	}
	@Override
	public int compareTo(Edge e) {
		return this.w - e.w;
	}
}
static Edge eList[] = new Edge[vNum+1];
public static int prim(int sV) {
	PriorityQueue<Edge> pQ = new PriorityQueue<>();
	pQ.add(new Edge(sV, 0)); // 시작 정점 저장
	boolean visited[] = new boolean[vNum+1]; // 해당 정점을 간선으로 연결해줬는지 확인
	Edge e;
	int totW = 0;
	while(!pQ.isEmpty()) {
		e = pQ.remove(); // 간선
		if(!visited[e.v]) { // 방문 유무에 따라 그래프에 사이클이 생기는지가 결정
			visited[e.v] = true;
			totW += e.w;
			for(Edge next : eList[e.v])
				if(!visited[next.v])
					pQ.add(next); // 방문하지 않은 해당 정점으로 부속된 간선 큐에 저장
		}
	}
	return totW; // MST 가중치 합
}
```
- 시간 복잡도 : `O(E * logV)`
  - E : 간선의 수, V : 정점의 수


### 참고
- [[Algorithms] Prim's Algorithm | 프림 알고리즘](https://dad-rock.tistory.com/646)
- [[알고리즘] 프림 알고리즘(Prim Algorithm) - JAVA / 자바](https://kwin0825.tistory.com/77)
