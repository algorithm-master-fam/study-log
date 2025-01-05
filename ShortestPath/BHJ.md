# 최단 경로(Shortest Path Algorithm)

## 1. 다익스트라(Dijkstra)

### 개념

- 단일 출발지 최단 경로 알고리즘으로, 가중치가 있는 그래프에서 출발 노드에서 다른 모든 노드까지의 최단 경로를 탐색
- 우선순위 큐(최소 힙)를 사용하여 현재까지의 최단 경로를 갱신함
- 음수 가중치가 있는 경우에는 사용할 수 없음

### 사용 예시

- 최단 거리 문제, 네비게이션 시스템, 통신 네트워크 등

### 시간 복잡도

- $V$는 정점의 수, $E$는 간선의 수
- 인접 리스트를 사용하는 경우: $O((V + E) \log V)$
- 인접 행렬을 사용하는 경우: $O(V^2)$

```python
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n + 1)]
# 방문한 적이 있는지 체크하는 목적의 리스트를 만들기
visited = [False] * (n + 1)
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n + 1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[a].append((b, c))

# 방문하지 않은 노드 중에서, 가장 최단 거리가 짧은 노드의 번호를 반환
def get_smallest_node():
    min_value = INF
    index = 0 # 가장 최단 거리가 짧은 노드(인덱스)
    for i in range(1, n + 1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = i
    return index

def dijkstra(start):
    # 시작 노드에 대해서 초기화
    distance[start] = 0
    visited[start] = True
    for j in graph[start]:
        distance[j[0]] = j[1]
    # 시작 노드를 제외한 전체 n - 1개의 노드에 대해 반복
    for i in range(n - 1):
        # 현재 최단 거리가 가장 짧은 노드를 꺼내서, 방문 처리
        now = get_smallest_node()
        visited[now] = True
        # 현재 노드와 연결된 다른 노드를 확인
        for j in graph[now]:
            cost = distance[now] + j[1]
            # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[j[0]]:
                distance[j[0]] = cost

# 다익스트라 알고리즘을 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n + 1):
    # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
    if distance[i] == INF:
        print("INFINITY")
    # 도달할 수 있는 경우 거리를 출력
    else:
        print(distance[i])
```

## 2. 벨만-포드(Bellman-Ford)

### 개념

- 단일 출발지 최단 경로 알고리즘으로, 음수 가중치를 가진 그래프에서도 작동
- 각 노드에 대한 최단 경로를 반복적으로 갱신하여 최종적으로 모든 노드에 대한 최단 경로를 구함
- 음수 사이클을 탐지 가능

### 사용 예시

- 음수 가중치가 포함된 그래프의 최단 경로 문제, 금융 네트워크에서의 사이클 탐지 등

### 시간 복잡도

- $V$는 정점의 수, $E$는 간선의 수
- $O(V \cdot E)$

```python
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 모든 간선에 대한 정보를 담는 리스트 만들기
edges = []
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n + 1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    edges.append((a, b, c))

def bf(start):
    # 시작 노드에 대해서 초기화
    distance[start] = 0
    # 전체 n - 1번의 라운드(round)를 반복
    for i in range(n):
        # 매 반복마다 "모든 간선"을 확인하며
        for j in range(m):
            cur_node = edges[j][0]
            next_node = edges[j][1]
            edge_cost = edges[j][2]
            # 현재 간선을 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if distance[cur_node] != INF and distance[next_node] > distance[cur_node] + edge_cost:
                distance[next_node] = distance[cur_node] + edge_cost
                # n번째 라운드에서도 값이 갱신된다면 음수 순환이 존재
                if i == n - 1:
                    return True
    return False

# 벨만 포드 알고리즘을 수행
negative_cycle = bf(1) # 1번 노드가 시작 노드

if negative_cycle:
    print("-1")
else:
    # 1번 노드를 제외한 다른 모든 노드로 가기 위한 최단 거리를 출력
    for i in range(2, n + 1):
        # 도달할 수 없는 경우, -1을 출력
        if distance[i] == INF:
            print("-1")
        # 도달할 수 있는 경우 거리를 출력
        else:
            print(distance[i])
```

## 3. A*

### 개념

- 최단 경로 탐색을 위한 휴리스틱 기반 알고리즘
- 다익스트라 알고리즘의 변형으로, 현재까지의 경로 비용과 목표 지점까지의 예상 비용(휴리스틱)을 결합하여 경로를 탐색
- 특히 그래프의 구조가 복잡할 때 효율적

### 사용 예시

- 게임 AI에서의 경로 탐색, 로봇 경로 계획, 네비게이션 시스템 등

### 시간 복잡도

- $E$는 간선의 수
- 최악의 경우: $O(E)$ (휴리스틱의 품질에 따라 실제 성능은 향상될 수 있음)

```python
// GPT 참고 코드
import heapq

def a_star(graph, start, goal, heuristic):
    open_set = [(0, start)]
    g_score = {node: float('inf') for node in graph}
    g_score[start] = 0

    while open_set:
        _, current = heapq.heappop(open_set)

        if current == goal:
            return g_score[goal]

        for neighbor, weight in graph[current].items():
            tentative_g_score = g_score[current] + weight
            if tentative_g_score < g_score[neighbor]:
                g_score[neighbor] = tentative_g_score
                f_score = tentative_g_score + heuristic(neighbor, goal)
                heapq.heappush(open_set, (f_score, neighbor))

    return float('inf')

# 예제 그래프 및 휴리스틱
graph = {
    'A': {'B': 1, 'C': 4},
    'B': {'A': 1, 'C': 2, 'D': 6},
    'C': {'A': 4, 'B': 2, 'D': 3},
    'D': {}
}

def heuristic(node, goal):
    return 0  # 단순화된 휴리스틱 예제

print(a_star(graph, 'A', 'D', heuristic))
```

## 4. 플로이드-워샬(Floyd-Warshall)

### 개념
- 모든 쌍의 최단 경로를 찾기 위한 알고리즘
- 동적 프로그래밍을 사용하여 두 노드 간의 최단 경로를 계산
- 모든 노드 쌍에 대해 경로를 갱신하므로, 그래프의 모든 노드 간의 최단 경로를 구할 수 있음

### 사용 예시

- 네트워크의 모든 쌍 최단 경로 문제, 도시 간 거리 계산 등

### 시간 복잡도
- $V$는 정점의 수
- $O(V^3)$

```python
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수 및 간선의 개수를 입력받기
n = int(input())
m = int(input())
# 2차원 리스트(그래프 표현)를 만들고, 모든 값을 무한으로 초기화
graph = [[INF] * (n + 1) for _ in range(n + 1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n + 1):
    for b in range(1, n + 1):
        if a == b:
            graph[a][b] = 0

# 각 간선에 대한 정보를 입력 받아, 그 값으로 초기화
for _ in range(m):
    # A에서 B로 가는 비용은 C라고 설정
    a, b, c = map(int, input().split())
    graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘을 수행
for k in range(1, n + 1):
    for a in range(1, n + 1):
        for b in range(1, n + 1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행된 결과를 출력
for a in range(1, n + 1):
    for b in range(1, n + 1):
        # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
        if graph[a][b] == 1e9:
            print("INFINITY", end=" ")
        # 도달할 수 있는 경우 거리를 출력
        else:
            print(graph[a][b], end=" ")
    print()
```
