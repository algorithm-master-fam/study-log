친구를 맺어주는 소셜 네트워크 서비스를 만든다고 가정하자.
박지현이 배희진의 친구라면 배희진 역시 박지현의 친구일 때 이러한 관계를 "상호적인 관계"이라고 부른다.
위 같은 데이터를 가장 잘 조작하는 방법은 무엇일까?
간단한 접근 방법으론 2차원 배열에 친구 관계 리스트를 저장하는 것이다.
한 유저당 친구가 몇 명 없다면 위 방식으로 친구 관계를 찾아낼 수 있지만, 여러 명이 된다면?
컴퓨터는 리스트 내 관계를 일일이 찾아야 하고, 이는 O(N)의 시간복잡도가 걸릴 것이다.
이를 해결할 방법이 Graph라는 자료 구조이다.

## Graph란?
> : Graph는 정점(Vertex)과 간선(Edge)으로 구성된 데이터 구조   
> 그래프는 다양한 문제를 해결하는 데 사용되며,
> 1) 소셜 네트워크 분석
> 2) 지도 경로 탐색
> 3) 스케줄링 등에서 활용 


---


### 1. 그래프의 주요 특징
> _G = (V, E)_   
정점의 집합 V와 간선의 집합을 E라고 할 때, 그래프 G는 V와 E의 집합(V, E)라는 의미 
> ![스크린샷 2024-12-08 오후 3.27.43.png](..%2F..%2F..%2F..%2F..%2F..%2Fvar%2Ffolders%2Fph%2F_z8zjw6x6bggjw1q_n4bv4x80000gn%2FT%2FTemporaryItems%2FNSIRD_screencaptureui_HPL0US%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202024-12-08%20%EC%98%A4%ED%9B%84%203.27.43.png)  
> 위 그림을 볼 때,   
> - V(G) = {1, 2, 3, 4, 5}  
> - E(G) = {(1,2), (3,1), (3,2), (4,1), (5,2), (5,4)}  
> => V(G)를 그래프 G의 정점 집합, E(G)는 그래프 G의 간선 집합  


- **정점(Vertex)**: 그래프의 각 점 = 노드 = 데이터 저장 
- **간선(Edge)**: 정점 간의 연결하는 선 
- **가중치(Weight)**: 간선에 부여된 값 (선택적)
- **차수(Degree)**: 무방향 그래프에서 하나의 정점에 붙어있는 간선 개수
- **인접(Adjacent)**: 정점 사이 간선 존재
- **단순 경로**: 출발지->목적지까지 가는 경로 중 반복되는 정점x  = 한 붓 그리기
- **사이클(Cycle)**: 단순 경로의 출발지가 목적지와 같은 경우   
- 방향 여부에 따라 방향 그래프 or 무방향 그래프로 나뉨 

---
### 2. 그래프 종류  

1. 무방향 그래프(Undirected Graph)  
: - 간선에 방향이 없는 그래프를 의미  
- 정점 v와 정점 w를 연결하는 간선을 (v, w)라고 할 때, `(v, m) = (w, v)` 같은 간선을 의미  
- 정점이 n개일 때 무방향 그래프가 가질 수 있는 최대 간선 수는 `n(n-1)/2` 

2. 방향 그래프(Directed Graph)
: - 간선에 방향이 있는 그래프를 의미  
- 정점 v에서 w로 가는 간선을 (v, w)라고 할 때, `(v, m) != (w, v)` 같은 간선을 의미하지 않음   
- 정점이 n개일 때 방향 그래프가 가질 수 있는 최대 간선 수는 `n(n-1)`

3. 완전 그래프(Complete Graph)
: - 모든 정점에 간선이 존재하고, 모든 정점이 서로 연결된 그래프를 의미  

4. 가중치 그래프(Weighted Graph)  
: - 간선 내 비용(=가중치)이 존재하는 그래프  

![스크린샷 2024-12-08 오후 3.39.11.png](..%2F..%2F..%2F..%2F..%2F..%2Fvar%2Ffolders%2Fph%2F_z8zjw6x6bggjw1q_n4bv4x80000gn%2FT%2FTemporaryItems%2FNSIRD_screencaptureui_TQNa3T%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202024-12-08%20%EC%98%A4%ED%9B%84%203.39.11.png)

---

### 3. 그래프 vs 트리
- 그래프 
  - 사이클(순환)을 가질 수 있다
  - 모든 정점이 반드시 연결되어 있지 않을 수 있다
  - 정점과 간선으로 이루어진 일반적인 데이터 구조
- 트리
  - 사이클이 없는 연결 그래프
  - N개의 정점이 있을 때 항상 N-1개의 간선을 가진다
  - 루트(Root)라는 시작 정점이 있다

---

### 4. 그래프 구현

#### 4-1. 인접 리스트 (Adjacency List)
인접 리스트는 각 정점에 연결된 다른 정점을 리스트로 표현 가능  
=> 메모리 효율적이며 연결된 정점을 빠르게 찾을 수 있다는 장점 존재  

```java
import java.util.*;

class Graph {
    private Map<Integer, List<Integer>> adjList = new HashMap<>();

    public void addEdge(int v1, int v2) {
        adjList.computeIfAbsent(v1, k -> new ArrayList<>()).add(v2);
        adjList.computeIfAbsent(v2, k -> new ArrayList<>()).add(v1); // 무방향 그래프
    }

    public List<Integer> getNeighbors(int v) {
        return adjList.getOrDefault(v, new ArrayList<>());
    }

    public void printGraph() {
        for (int vertex : adjList.keySet()) {
            System.out.println(vertex + " -> " + adjList.get(vertex));
        }
    }
}
```

#### 4-2. 인접 행렬 (Adjacency Matrix)
인접 행렬은 정점 간의 연결 관계를 2차원 배열로 표현 가능  
=> 특정 정점 간 연결 여부를 O(1)로 확인 가능  

```java  
class GraphMatrix {
    private int[][] adjMatrix;
    private int size;

    public GraphMatrix(int size) {
        this.size = size;
        this.adjMatrix = new int[size][size];
    }

    public void addEdge(int v1, int v2) {
        adjMatrix[v1][v2] = 1;
        adjMatrix[v2][v1] = 1; // 무방향 그래프
    }

    public void printMatrix() {
        for (int i = 0; i < size; i++) {
            for (int j = 0; j < size; j++) {
                System.out.print(adjMatrix[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```

---

### 5. 그래프 순회

그래프 순회란 한 정점에서 출발해 그래프의 모든 정점을 한 번씩 방문하는 것이다.    
그래프 탐색 방법은 크게 **DFS(깊이 우선 탐색)와 BFS(너비 우선 탐색)**으로 나뉜다.  

#### 5-1. 깊이 우선 탐색(DFS, Depth-First-Search)  
- 정점(V) 방문  
- 정점(V)의 인접 정점 중 방문하지 않은 정점을 찾아 DFS를 재귀적 수행  

#### 5-2. 너비 우선 탐색(BFS, Breadth-First-Search)
- 정점(V) 방문 후, 큐 삽입
- 정점(V)의 인접 정점 중 방문하지 않은 정점을 차례대로 방문  
- 2번 과정이 종료되면, 큐에 있는 정점을 꺼낸 후 다시 2번 스텝부터 수행  

---

### 6. 최소 신장 트리 (Minimum Spanning Tree, MST)
> -  신장 트리란, 그래프 G의 부분 그래프로서 G의 모든 정점을 포함하는 트리를 의미  
> - 최소 신장 트리란, 모든 정점을 연결하는 간선들의 부분 집합 중, 가중치의 합이 최소가 되는 트리를 의미  

#### 최소 신장 트리 조건  
1) 모든 정점으로 갈 수 있는 경로가 존재하는 서브 그래프일 때 
2) 간선 가중치 합 최소일 때  

주어진 가중치 그래프에서 최소 신장 트리로 만드는 대표적 알고리즘은 아래와 같다.   
  1) Kruskal: 간선을 정렬한 후 최소 간선을 선택
  2) Prim: 정점을 기준으로 최소 간선을 선택

두 알고리즘 모두 Greedy(탐욕 알고리즘)을 사용하며, 각 단계에서 최상의 선택을 하고, 한 번 내린 결정을 번복하지 않는다는 특징이 존재한다.  

---

### 7. 다익스트라(Dijkstra) 알고리즘
> - 다익스트라 알고리즘이란, 단일 시작점에서 다른 모든 정점까지의 최단 경로를 탐색하는 알고리즘  

```java
    class Dijkstra {
        public int[] dijkstra(int n, int[][] edges, int start) {
            int[] dist = new int[n];
            Arrays.fill(dist, Integer.MAX_VALUE);
            dist[start] = 0;
    
            PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[1]));
            pq.offer(new int[]{start, 0});
    
            while (!pq.isEmpty()) {
                int[] current = pq.poll();
                int node = current[0];
                int distance = current[1];
    
                for (int[] edge : edges) {
                    if (edge[0] == node) {
                        int next = edge[1];
                        int weight = edge[2];
                        if (dist[next] > distance + weight) {
                            dist[next] = distance + weight;
                            pq.offer(new int[]{next, dist[next]});
                        }
                    }
                }
            }
            return dist;
        }
    }
```
---

### 벨만포드 알고리즘과 플로이드-워샬 알고리즘
다익스트라 알고리즘과 마찬가지로 최단 경로를 구할 수 있는 또 다른 알고리즘이 존재한다.  
최단 경로란, 가중치 방향 그래프에서 출발지 -> 도착지까지 경로의 간선 가중치 합이 최소인 경우를 의미한다.  
단, 무방향 그래프인 경우 (V, W) != (W, V)를 다른 간선으로 구분하여 구분해야 한다.  

- 벨만-포드(Bellman-Ford) 알고리즘
  - 음수 가중치가 있는 그래프 중 최단 경로 찾을 수 있는 알고리즘  
  - 시간 복잡도 : O(V*E)
- 플로이드-워샬(Floyd-Warshall) 알고리즘 
  - 모든 정점 쌍 간 최단 경로를 계산할 수 있는 알고리즘  
  - 시간 복잡도: O(V^2)  
