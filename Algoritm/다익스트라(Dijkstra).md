# ✈️ 다익스트라(Dijkstra)

가중치 그래프에서 한 정점으로부터 모든 정점의 최단거리를 구하는 알고리즘  
(가중치에 음수가 존재하면 안된다는 제약사항이 존재)

<br>

## 1. 원리

아래 2가지 작업을 모든 정점을 모두 방문할 때까지 반복한다.

> 1. 방문하지 않은 정점 중, 가장 cost가 작은 정점을 방문한다.  
> 2. 해당 정점과 연결된 정정들 중에서 거리가 이전에 기록한 값보다 작다면 값을 갱신한다.  

<br>


## 2. 과정


![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/4d3e3236-099f-4213-88c1-a25fe5ca8ec3)

**(1) 6개의 정점이 있고, 각 정점 사이의 cost가 위와 같은 그래프에서  
　　0번 정점에 대한 모든 정점과의 최단거리를 구해보자**


<br>


![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/448a7f99-20a2-40dc-b75e-8ef1796fb8e1)

**(2) 최단거리 저장 배열 dist를 무한대값으로 초기화하고,  
　　0번에 대해서는 자기자신이므로 0으로 설정**

<br>

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/2503be23-6d4d-4776-89d5-3be150735fe2)

**(3) 0번 정점 방문 → 그와 연결된 1번, 3번 정점의 거리 계산**  
> '0번~1번의 최단거리' + '1번~3번 거리' = 25와  
> '1번~3번 거리'(현재 dist값) 비교

<br>

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/5248c765-f726-4854-b523-152c88c5e5ee)

**(4) 다음 정점 방문(최소값을 얻은 1번 정점 우선 방문)**
> dist[2] = Math.min('0번~1번의 최단거리' + '1번~2번 거리', dist[2])  
> dist[3] = Math.min('0번~1번의 최단거리' + '1번~3번 거리', dist[3])


<br>

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/cd2b7ad8-3b3a-44e0-8f25-e9fbb2fdefda)

**(5) 2번 정점은 연결된 인접정점이 없으므로 넘어간다.**

<br>

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/454eab16-2854-4214-81ff-54ac3ac8fcc4)

**(6) 바로 다음 3번 정점으로 넘어가서 4번 정점과의 거리를 구한다.**  
> '0번~3번 최단거리' + '3번~4번 거리' = 30 <  dist[4] 이므로  
> dist[4]는 30으로 갱신


<br>

![image](https://github.com/SeoYeonBae/CS_study/assets/63834758/f5ab4ab2-83ff-4a60-840d-9fd7ee6cc5ff)

**(7) 5번 정점은 0번으로부터 갈 수 없으므로 INF값 그대로  가고,  
　갈 수 있는 모든 정점을 방문하였으므로 알고리즘 종료**

<br>

> [전체 과정 요약]
> - 방문할 정점 정하기(작은 cost의 정점 우선)
> - 현재 정점 i, 방문한 정점 j
> - **Math.min(dist[i] + graph[i->j], dist[j])**


<br>


## 3. 예제 코드

```



```


<br>

## 4. 시간복잡도


<br>



<hr>

#### 참고자료

- [다익스트라 알고리즘(Dijikstra's Algorithm)](https://currygamedev.tistory.com/18)
- [다익스트라 알고리즘](https://velog.io/@soulee__/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%8B%A4%EC%9D%B5%EC%8A%A4%ED%8A%B8%EB%9D%BC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
