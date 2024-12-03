# 그래프

## 그래프 정의

- 그래프는 아이템(사물 또는 추상적 개념)들과 이들 사이의 연결 관계를 표현한다.
- 그래프는 정점(vertex)들의 집합과 이들을 연결하는 간선(Edge)들의 집합으로 구성된 자료 구조
    - |V| : 정점의 개수, |E| : 그래프에 포함된 간선의 개수
    - |V| 개의 정점을 가지는 그래프는 최대 |V| (|V|-1) / 2 간선이 가능
    - 예) 5개 정점이 있는 그래프의 최대 간선 수는 10(-5*4/2)개이다.
- 선형 자료구조나 트리 자료구조로 표현하기 어려운 N:N 관계를 가지는 원소들을 표현하기에 용이하다.

### 그래프 유형

- 무향 그래프(Undirected Graph)
- 유향 그래프(Directed Graph)
- 가중치 그래프(Weighted Graph)
- 사이클 없는 방향 그래프(DAG, Directed Acyclic Graph)
- 완전 그래프 : 정점들에 대해 가능한 모든 간선들을 가진 그래프
- 부분 그래프 : 원래 그래프에서 일부의 정점이나 간선을 제외한 그래프

### 그래프 경로

- 경로란 간선들을 순서대로 나열한 것
    - 간선들 : (0, 2), (2, 4), (4, 6)
    - 정점들 : 0 - 2 - 4 - 6
- 경로 중 한 정점을 최대한 한번만 지나는 경로를 단순경로라 한다.
    - 0 - 2 - 4 - 6, 0 - 1 - 6
- 시작한 정점에서 끝나는 경로를 사이클(cycle)이라고 한다.
    - 1 - 3 - 5 - 1

### 그래프 표현

- 간선의 정보를 저장하는 방식, 메모리나 성능을 고려해서 결정
- 인접 행렬(Adjacent matrix)
    - |V| X |V| 크기의 2차원 배열을 이용해서 간선 정보를 저장
    - 배열의 배열(포인터 배열)
- 인접 리스트(Adjacent List)
    - 각 정점마다 해당 정점으로 나가는 간선의 정보를 저장
- 간선의 배열
    - 간선(시작 정점, 끝 정점)을 배열에 연속적으로 저장

### 인접(Adjacency)

- 두 개의 정점에 간선이 존재(연결됨)하면 서로 인접해 있다고 한다.
- 완전 그래프에 속한 임의의 두 정점들은 모두 인접해 있다.

### 인접 행렬

- 두 정점을 연결하는 간선의 유무를 행렬로 표현
    - |V| X |V| 정방 행렬
    - 행 번호와 열 번호는 그래프의 정점에 대응
    - 두 정점이 인접되어 있으면 1, 그렇지 않으면 0으로 표현
    - 무향 그래프
        - i번째 행의 합 = i번째 열의 합 = V<sub>i</sub>의 차수
    - 유향 그래프
        - 행 i의 합 = V<sub>i</sub>의 진출 차수
        - 열 i의 합 = V<sub>i</sub>의 진입 차수

### 인접 리스트

- 각 정점에 대한 인접 정점들을 순차적으로 표현
- 하나의 정점에 대한 인접 정점들을 각각 노드로 하는 연결 리스트로 저장

```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

V, E = map(int, input().split())
arr = list(map(int, input.split()))
adjM = [[0]*(V+1) for _ in range(V+1)] # 인접 행렬
adjL = [[0] for _ in range(V+1)] # 인접 리스트
for i in range(E): # E개의 간선
    n1, n2 = arr[i*2], arr[i*2+1]
    adjM[n1][n2] = 1
    adjM[n2][n1] = 1 # <- 방향성이 없다면
    adjL[n1].append(n2)
    adjL[n2].append(n1) # <- 방향성이 없다면
print()
```

## DFS(Depth First Search)

### 재귀

```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

def dfs1(v, k): # 중복 없이 빠짐 없이
    visited[v] = 1 # 중복 방지
    print(v)
    for w in range(1, k+1):
        if adjM[v][w] == 1 and visited[w] == 0:
            dfs1(w, k)
    # for w in adjL[v]: # v와 인접하고
    #     if visited[w] == 0: # 방문한 적이 없는 w가 있다면
    #         dfs1(w, k)

V, E = map(int, input().split())
arr = list(map(int, input().split()))
adjM = [[0]*(V+1) for _ in range(V+1)] # 인접 행렬
adjL = [[] for _ in range(V+1)] # 인접 리스트
for i in range(E): # E개의 간선
    n1, n2 = arr[i*2], arr[i*2+1]
    adjM[n1][n2] = 1
    adjM[n2][n1] = 1 # <- 방향성이 없다면
    # adjL[n1].append(n2)
    # adjL[n2].append(n1) # <- 방향성이 없다면

visited =[0]*(V+1) # 중복 방지

dfs1(1, V)
```

### 반복

```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

def dfs2(s, k):
    stack = []
    visited = [0]*(k+1)
    v = s
    while True:
        if visited[v] == 0:
            print(v)
            visited[v] = 1
        for w in range(1, k+1):
            if adjM[v][w] and visited[w] == 0:
                stack.append(v)
                v = w
                break
        else: # 더 이상 인접인 정점이 없으면
            if stack: # 스택이 비어있지 않으면
                v = stack.pop()
            else: # 스택이 비어 있으면
                break
    return

V, E = map(int, input().split())
arr = list(map(int, input().split()))
adjM = [[0]*(V+1) for _ in range(V+1)] # 인접 행렬
adjL = [[] for _ in range(V+1)] # 인접 리스트
for i in range(E): # E개의 간선
    n1, n2 = arr[i*2], arr[i*2+1]
    adjM[n1][n2] = 1
    adjM[n2][n1] = 1 # <- 방향성이 없다면
    # adjL[n1].append(n2)
    # adjL[n2].append(n1) # <- 방향성이 없다면

visited =[0]*(V+1) # 중복 방지

dfs2(1, V)
```

### 목적지까지 갈 수 있는 경로의 개수

```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

def dfs3(v, k, g):
    global cnt
    if v == g: # 도착한 곳이 목적지라면
        cnt += 1
    else:
        visited[v] = 1 # 중복 방지
        for w in range(1, k+1):
            if adjM[v][w] == 1 and visited[w] == 0:
                dfs3(w, k, g)
        visited[v] = 0 # 목적지까지의 다른 경로를 찾기 위해

V, E = map(int, input().split())
arr = list(map(int, input().split()))
adjM = [[0]*(V+1) for _ in range(V+1)] # 인접 행렬
adjL = [[] for _ in range(V+1)] # 인접 리스트
for i in range(E): # E개의 간선
    n1, n2 = arr[i*2], arr[i*2+1]
    adjM[n1][n2] = 1
    adjM[n2][n1] = 1 # <- 방향성이 없다면
    # adjL[n1].append(n2)
    # adjL[n2].append(n1) # <- 방향성이 없다면

visited =[0]*(V+1) # 중복 방지
cnt = 0
dfs3(1, V, 7)
print(cnt)
```

## BFS(Breadth First Search)

## 서로소 집합(Disjoint-sets)

- 서로소 또는 상호배타 집합들은 서로 중복 포함된 원소가 없는 집합들이다. 다시 말해 교집합이 없다.
- 집합에 속한 하나의 특정 멤버를 통해 각 집합들을 구분한다. 이를 대표자(representative)라 한다.
- 상호배타 집합을 표현하는 방법
    - 연결 리스트, 트리
- 상호배타 집합 연산
    - `Make-Set(x)`, `Find-Set(x)`, `Union(x, y)`
    - Find-Set(y) : y가 속한 집합의 대표 원소

```python
def find_set(x):
    while x != rep[x]: # x == rep[x]가 될 때까지
        x = rep[x]
    return x

def union(x, y): # y의 대표 원소가 x의 대표 원소를 가리키도록
    # rep[y] = find_set(x) (X)
    rep[find_set(y)] = find_set(x)

# makeset()
rep = [i for i in range(6)]

union(x, y)

print(rep)
```

### 상호 배타 집합 표현 - 연결 리스트

### 상호 배타 집합 표현 - 트리

- 하나의 집합(a disjoint set)을 하나의 트리로 표현한다.
- 자식 노드가 부모 노드를 가리키며 루트 노드가 대표자가 된다.

### 상호 배타 집합에 대한 연산

- Make-Set(x) : 유일한 멤버 x를 포함하는 새로운 집합을 생성하는 연산
- Find_Set(x) : x를 포함하는 집합을 찾는 연산
- Union(x, y) : x와 y를 포함하는 두 집합을 통합하는 연산

## 최소 비용 신장 트리(MST)

- 그래프에서 최소 비용 문제
    
    1) 모든 정점을 연결하는 간선들의 가중치의 합이 최소가 되는 트리
    
    2) 두 정점 사이의 최소 비용의 경로 찾기
    
- 신장 트리 : n개의 정점으로 이루어진 **무방향 그래프**에서 n개의 정점과 n-1개의 간선으로 이루어진 트리
- 최소 신장 트리 (Minimum Spanning Tree) : 무방향 가중치 그래프에서 신장 트리를 구성하는 간선들의 가중치의 합이 최소인 신장 트리

![MST1](https://github.com/user-attachments/assets/9250ca18-2e3f-4a06-907d-fe9b3e545ecc)

![MST2](https://github.com/user-attachments/assets/5baafffc-daad-4976-9220-388d8fccd66e)

### KRUSKAL 알고리즘

- 간선을 하나씩 선택해서 MST를 찾는 알고리즘
    
    1) 최초, 모든 간선을 가중치에 따라 오름차순으로 정렬
    
    2) 가중치가 가장 낮은 간선부터 선택하면서 트리를 증가시팀
    
    - 사이클이 존재하면 다음으로 가중치가 낮은 간선 선택
    
    3) n-1개의 간선이 선택될 때까지 2)를 반복
    

```python
'''
6 11
0 1 32
0 2 31
0 5 60
0 6 51
1 2 21
2 4 46
2 6 25
3 4 34
3 5 18
4 5 40
4 6 51
'''

V, E = map(int, input().split())

def find_set(x):
    while x != rep[x]: # x == rep[x]가 될 때까지
        x = rep[x]
    return x

def union(x, y): # y의 대표 원소가 x의 대표 원소를 가리키도록
    # rep[y] = find_set(x) (X)
    rep[find_set(y)] = find_set(x)

# makeset()
rep = [i for i in range(V+1)]

edge = []
for _ in range(E): # E개의 간선 정보
    v1, v2, w = map(int, input().split())
    edge.append([v1, v2, w])

# (1) 가중치를 기준으로 오름차순 정렬
edge.sort(key=lambda x:x[2])

# (2) N개 정점(V+1), N-1개의 간선 선택
N = V+1
s = 0 # MST에 포함된 간선의 가중치 합
cnt = 0
MST = []
for u, v, w in edge: # 가중치가 작은 것부터
    if find_set(u) != find_set(v): # 사이클이 생기지 않으면
        cnt += 1
        s += w # 가중치 합
        MST.append([u, v, w])
        union(u, v)
        if cnt == N-1: # MST 구성 완료
            break

print(s)
print(MST)
```

## 최단 경로

- 최단 경로 정의
    - 간선의 가중치가 있는 그래프에서 두 정점 사이의 경로들 중에 간선의 가중치의 합이 최소인 경로
- 하나의 시작 정점에서 끝 정점까지의 최단 경로
    - 다익스트라(dijkstra) 알고리즘 : 음의 가중치를 허용하지 않음
    - 벨만-포드(Bellman-Ford) 알고리즘 : 음의 가중치 허용
- 모든 정점들에 대한 최단 경로
    - 플로이드-워샬(Floyd-Warshall) 알고리즘

### Dijkstra 알고리즘

- 시작 정점에서 거리가 최소인 정점을 선택해 나가면서 최단 경로를 구하는 방식이다.
- 시작 정점(s)에서 끝정점(t)까지의 최단 경로에 정점 x가 존재한다.
- 이때, 최단 경로는 s에서 x까지의 최단 경로와 x에서 t까지의 최단 경로 구성된다.
- 탐욕 기법을 사용한 알고리즘으로 MST의 프림 알고리즘과 유사하다.

```python
'''
5 8
0 1 2
0 2 4
1 2 1
1 3 7
2 4 3
3 4 2
3 5 1
4 5 5
'''
def dijkstra(s, V): # s 출발, V 마지막 정점 번호
    U = [0]*(V+1) # U 최소비용이 결정된 정점 집합
    U[s] = 1 # U = {s}

    for i in range(V+1): # s에서 나머지 정점 i로 가는 비용 복사
        D[i] = adjM[s][i]

    # while U != V 남은 정점의 비용 결정
    N = V+1 # N개의 정점
    for _ in range(N-1): # N-1개 정점의 비용 결정
        # D[w]가 최소인 w 결정
        minV = INF
        w = 0
        for i in range(V+1):
            if U[i] == 0 and minV > D[i]: # 남은 정점 i 중, 비용이 확정되지 않았고 최소값이라면
                w = i
                minV = D[i]
        U[w] = 1 # 최소인 w는 최소 비용 확정
        # w에 인접인 정점에 대해, 기존 비용 vs w를 거쳐가는 비용 비교
        for v in range(V+1):
            if 0 < adjM[w][v] < INF: # w에 인접인 v의 조건
                D[v] = min(D[v], D[w]+adjM[w][v]) # 기존 비용 vs w를 거쳐가는 비용 비교

INF = 10000 # 문제에 따라
V, E = map(int, input().split()) # 0~V번 정점, E 간선 수
adjM = [[INF]*(V+1) for _ in range(V+1)]
for i in range(V+1):
    adjM[i][i] = 0 # 자기 자신으로 가는 비용
for _ in range(E):
    u, v, w = map(int, input().split()) # u -> v, w 가중치
    adjM[u][v] = w

D = [0]*(V+1)

dijkstra(0, V)
print(D)
```
