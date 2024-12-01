# 우선순위 큐(Priority Queue)

## 트리(Tree)

### 개념

- 비선형 구조
- 원소들 간에 1:n 관계를 가지고 자료구조
- 원소들 간에 계층관계를 가지는 계층형 자료구조
- 상위 원소에서 하위 원소로 내려가면서 확장되는 트리(나무)모양의 구조
- 한 개 이상의 노드로 이루어진 유한 집합이며 다음 조건을 만족
    - 노드 중 최상위 노드를 루트(root)라 한다.
    - 나머지 노드들은 n(≥0)개의 분리 집합 T1, … , TN으로 분리될 수 있다.
- 이들 T1, … , TN은 각각 하나의 트리가 되며(재귀적 정의) 루트의 부트리(subtree)라 한다.

### 용어

- 노드(node) - 트리의 원소
- 간선(edge) - 노드를 연결하는 선, 부모 노드와 자식 노드를 연결
- 루트 노드(root node) - 트리의 시작 노드
- 형제 노드(sibling node) - 같은 부모 노드의 자식 노드들
- 조상 노드 - 간선을 따라 루트 노드까지 이르는 경로에 있는 모든 노드들
- 서브 트리(subtree) - 부모 노드와 연결된 간선을 끊었을 때 생성되는 트리
- 자손 노드 - 서브 트리에 있는 하위 레벨의 노드들
- 차수(degree)
    - 노드의 차수 : 노드에 연결된 자식 노드의 수
    - 트리의 차수 : 트리에 있는 노드의 차수 중에서 가장 큰 값
    - 단말 노드(리프 노드) : 차수가 0인 노드, 자식 노드가 없는 노드

### 높이

- 노드의 높이 : 루트에서 노드에 이르는 간선의 수, 노드의 레벨
- 트리의 높이 : 트리에 있는 노드의 높이 중에서 가장 큰 값, 최대 레벨

## 👨‍👧‍👦 이진 트리(Binary Tree)

- 모든 노드들이 2개의 서브 트리를 갖는 특별한 형태의 트리
- **각 노드가 자식 노드를 최대한 2개까지만 가질 수 있는 트리**

### 특성

- 레벨 n에서의 노드의 최대 개수는 2<sup>n</sup>
- 높이가 h인 이진 트리가 가질 수 있는 노드의 최소 개수는 (h+1)개가 되며, 최대 개수는 2<sup>(h+1)</sup>-1개

### 종류

- **포화 이진 트리(Full Binary Tree)**
    - 모든 레벨에 노드가 포화 상태로 차 있는 이진 트리
    - 높이가 h일 때, 최대의 노드 개수인 2^<sup>(h+1)</sup>-1의 노드를 가진 이진 트리
    - 루트를 1번으로 하여 2<sup>(h+1)</sup>-1까지 정해진 위치에 대한 노드 번호를 가짐
- **완전 이진 트리(Complete Binary Tree)**
    - 높이가 h이고 노드 수가 n개일 때 (단, 2<sup>h</sup> ≤ n < 2<sup>(h+1)</sup>-1), 포화 이진 트리의 노드 번호 1번부터 n번까지 빈 자리가 없는 이진 트리
- **편향 이진 트리(Skewed Binary Tree)**
    - 높이 h에 대한 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가진 이진 트리
    - 선형 자료구조와 차이가 없음, 즉 트리의 특성이 없는 트리

## ⭐ **순회(Traversal)**

- 트리는 비선형 구조이기 때문에 선형 구조에서와 같이 선후 연결 관계를 알 수 없다.
- 따라서 특별한 방법이 필요하다.
- 순회란? 트리의 각 노드를 **중복되지 않게 전부 방문(visit)하는 것**을 말한다.
- 3가지의 기본적인 순회 방법
    - **전위 순회(preorder traversal) : VLR**
        - 부모 노드 방문 후, 자식 노드를 좌/우 순서로 방문한다.
    - **중위 순회(inortder traversal) : LVR**
        - 왼쪽 자식 노드, 부모 노드, 오른쪽 자식 노드 순으로 방문한다.
    - **후위 순회(postorder traversal) : LRV**
        - 자식 노드를 좌우 순서로 방문한 후, 부모 노드로 방문한다.

```python
**## 전위 순회(preorder traversal)**
def inorder_traverse(T):
    if T:                           # T is not None
        visit(T)                    # print(T.item)
        inorder_traverse(T.left)
        inorder_traverse(T.right)

**## 중위 순회(inortder traversal)**
def inorder_traverse(T):
    if T:                           # T is not None
        inorder_traverse(T.left)
        visit(T)                    # print(T.item)
        inorder_traverse(T.right)

**## 후위 순회(postorder traversal)**
def inorder_traverse(T):
    if T:                           # T is not None
        inorder_traverse(T.left)
        inorder_traverse(T.right)
        visit(T)                    # print(T.item)
```

## 이진 트리의 표현 - 배열

- 이진 트리에 각 노드 번호를 다음과 같이 부여
- 루트의 번호를 1로 함
- 레벨 n에 있는 노드에 대하여 왼쪽부터 오른쪽으로 2<sup>(n+1)</sup>부터 2<sup>(n+1)</sup>-1까지 번호를 차례로 부여
- 노드 번호를 배열의 인덱스로 사용
- 높이가 h인 이진 트리를 위한 배열의 크기는?
- 노드 번호의 성질
    - 노드 번호가 i인 노드의 부모 노드 번호 : **⌊**i/2**⌋ (**floor 연산 : x보다 작은 연산 중에 가장 큰 값**)**
    - 노드 번호가 i인 노드의 왼쪽 자신 노드 번호? 2*i
    - 노드 번호가 i인 노드의 오른쪽 자식 노드 번호? 2*i + 1
    - 레벨 n의 노드 번호 시작 번호는? 2<sup>n</sup>

## [참고] 이진 트리의 저장

⭐ 주의 : 당연하지만!

1. 루트 노드가 1이 아닌 경우 있음
2. 포화/완전 이진트리 형태가 아닌 경우 있음
3. 연속적인 숫자로 이루어진 노드가 아닌 경우 있음
4. 기타 등등 편견 버리기

```python
'''
4 <- 간선의 개수 N (항상 노드의 개수보다 1개 적음)
1 2 1 3 3 4 3 5
p c p c p c p c
'''
```

| **부모(p)** | 0 | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- | --- |
| **자식1(c1)** | 0 | 2 | 0 | 4 | 0 | 0 |
| **자식2(c2)** | 0 | 3 | 0 | 5 | 0 | 0 |

```python
## ▲ 부모 번호를 인덱스로 자식 번호를 저장
for i : 1 -> N
    read p, c
    if(c1[p] == 0):
        c1[p] = c
    else
        c2[p] = c:
```

| **자식(c)** | 0 | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- | --- |
| **부모(par)** | 0 | 0 | 1 | 1 | 3 | 3 |

```python
## ▲ 자식 번호를 인덱스로 부모 번호를 저장
for i : 1 -> N
    read p, c
    par[c] = p
```

| **자식(c)** | 0 | **1** |  | 2 |  | **3** |  | 4 |  | **5** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  |  | ↓ | ↖ | ← |  | ↓ | ↖ | ← |  | ↓ |
| **부모(a)** | 0 | **0** |  | 1 | ↖ | **1** |  | 3 | ↖ | **3** |

```python
## ▲ 루트 찾기, 조상 찾기
c = 5 # 5번 노드의 조상 찾기
while(a[c] != 0): # 루트인지 확인
    c = a[c]
    anc.append(c) # 조상 목록
root = c
```

### 배열을 이용한 이진 트리 표현의 단점

- 편향 이진 트리의 경우에는 사용하지 않는 배열 원소에 대한 메모리 공간 낭비 발생
- 트리의 중간에 새로운 노드를 삽입하거나, 기존의 노드를 삭제할 경우 배열의 크기 변경이 어려워 비효율적

### [참고] 이진 트리 순회 구현

```python
def preorder(i):
    if i:
        print(i, end = ' ')
        preorder(left[i])
        preorder(right[i])
    return

def inorder(i):
    if i:
        inorder(left[i])
        print(i, end = ' ')
        inorder(right[i])
    return

def postorder(i):
    if i:
        postorder(left[i])
        postorder(right[i])
        print(i, end = ' ')
    return

V = int(input())
arr = list(map(int, input().split()))
E = V-1 # 간선 수

left = [0]*(V+1) # 부모를 인덱스로 왼쪽 자식 저장
right = [0]*(V+1) # 부모를 인덱스로 오른쪽 자식 저장
par = [0]*(V+1) # 자식을 인덱스로 부모 저장
# chlid = [[] for _ in range(V+1)]

for i in range(E):
    p, c = arr[i*2], arr[i*2+1]
    if left[p] == 0:
        left[p] = c
    else:
        right[p] = c
    par[c] = p
    # child[p].append(c)

root = 1
while par[root] != 0: # 부모가 없는 정점을 찾을 때까지
    root += 1

preorder(root)
print()
inorder(root)
print()
postorder(root)
print()
```

## 수식트리

- 수식을 표현하는 이진 트리
- 수식 이진 트리(Expression Binary Tree)라고 부르기도 함
- 연산자는 루트 노드이거나 가지 노드
- 피연산자는 모두 잎 노드

### 수식 트리의 순회 (코드 구현 추가)

- 중위 순회 : A/B*C*D+E(식의 중위 표기법)
- 후위 순회 : AB/C*D*E+(식의 후위 표기법)
- 전위 순회 : +**/ABCDE(식의 전위 표기법)

## 이진 탐색 트리(Bianry Search Tree)

- 탐색 작업을 효율적으로 하기 위한 자료구조
- 모든 원소는 **서로 다른 유일한 키**를 갖는다.
- key(왼쪽 서브 트리) < key(루트 노드) < key(오른쪽 서브 트리)
- 왼쪽 서브 트리와 오른쪽 서브 트리도 이진 탐색 트리
- 중위 순회하면 오름차순으로 정렬된 값을 얻을 수 있다.

#### 삭제 연산 (내용 추가)

#### 탐색 연산

- 루트에서 시작
- 탐색할 키 값 x를 루트 노드의 키 값과 비교한다.
- if 키 값 x = 루트 노드의 키 값 : 원하는 원소를 찾았으므로 탐색 연산 성공
- if 키 값 x < 루트 노드의 키 값 : 루트 노드의 왼쪽 서브 트리에 대해서 탐색 연산 수행
- if 키 값 x > 루트 노드의 키 값 : 루트 노드의 오른쪽 서브 트리에 대해서 탐색 연산 수행
- 서브 트리에 대해서 순환적으로 탐색 연산을 반복한다.

#### 삽입 연산

- 탐색 연산을 수행
- 삽입할 원소와 같은 원소가 트리에 있으면 삽입할 수 없으므로, 같은 원소가 트리에 있는지 탐색하여 확인
- 탐색에서 탐색 실패가 결정되는 위치가 십입 위치가 된다.
- 탐색 실패한 위치에 원소를 삽입한다.

### 성능

- 탐색(searching), 삽입(insertion), 삭제(deletion) 시간은 트리의 높이 만큼 시간이 걸린다.
    - O(h), h : BST의 깊이(height)
- 평균의 경우
    - 이진 트리가 균형적으로 생성되어 있는 경우
    - O(logn)
- 최악의 경우
    - 한쪽으로 치우친 경사 이진 트리의 경우
    - O(n)
    - 순차 탐색과 시간복잡도가 같다.
- 검색 알고리즘의 비교
    - 배열에서의 순차 검색 : O(N)
    - 정렬된 배열에서의 순차 검색 : O(N)
    - 정렬된 배열에서의 이진 탐색 : O(logN)
        - 고정 배열 크기와 삽입, 삭제 시 추가 연산 필요
    - 이진 탐색 트리에서의 평균 : O(logN)
        - 최악의 경우 : O(N)
        - 완전 이진 트리 또는 균형 트리로 바꿀 수 있다면 최악의 경우를 없앨 수 있다.
            - 새로운 원소를 삽입할 때 삽입 시간을 줄인다.
            - 평균과 최악의 시간이 같다. O(logn)
    - 해쉬 검색 : O(1)
        - 추가 저장 공간이 필요

## 힙(Heap)

- 완전 이진 트리에 있는 노드 중에서 키 값이 가장 큰 노드가 키 값이 가장 작은 노드를 찾기 위해서 만든 자료구조
- 힙의 키를 우선순위로 활용하여 우선순위 큐를 구현할 수 있다.
- 힙에서는 항상 루트 노드를 제거한다.

### 우선순위 큐(proriry queue)
#### 구현 방법
1. 단순 리스트 활용
2. 힙 활용
	- 데이터의 개수가 N개일 떄, 구현 방식에 따라서 시간 복잡도는 아래와 같다.

| 우선순위 큐 구현 방식 | 삽입 시간 | 삭제 시간 |
| :---: | :---: | :---: |
| 리스트 | O(1) | O(N) |
| 힙(Heap) | O(logN) | O(logN) |

 - 단순히 N개의 데이터를 힙에 넣은 후 다시 꺼내는 작업은 정렬과 동일하다. (힙 정렬)
	- 이 경우 시간 복잡도는 O(NlogN)
```python
import sys
import heapq
input = sys.stdin.readline

def heapsort(iterable):
	h = []
	result = []
	for value in iterable:
		heapq.heappush(h, value)
	for i in range(len(h)):
		result.append(heapq.heappop(h))
	return result

n = int(input())
arr = []

for i in range(n):
	arr.append(int(input()))

res = heapsort(arr)

for i in range(n):
	print(res[i])
```
### 최대 힙(max heap)

- **키 값이 가장 큰 노드를 찾기 위한** 완전 이진 트리
- (부모 노드의 키 값 > 자식 노드의 키 값)
- 루트 노드 : 키 값이 가장 큰 노드

### 최소 힙(min heap)

- **키 값이 가장 작은 노드를 찾기 위한** 완전 이진 트리
- (부모 노드의 키 값 < 자식 노드의 키 값)
- 루트 노드 : 키 값이 가장 작은 노드

```python
## 최대 힙
# 최대 100개의 키

def enq(n):
    global last
    last += 1               # 완전 이진 트리에 마지막 정점을 추가하고
    heap[last] = n          # 마지막 정점에 저장
    c = last                # 부모가 있고, 부모 > 자식 조건 검사를 위해
    p = c//2
    while p > 0 and  heap[p] < heap[c]:
        heap[p], heap[c] = heap[c], heap[p]
        c = p               # 옮긴 자리에서 부모와 비교하기 위해
        p = c//2
    return

def deq():
    global last
    tmp = heap[1]           # 루트 임시 저장
    heap[1] = heap[last]    # 마지막 정점의 값을 루트로 이동
    last -= 1               # 마지막 정점 삭제
    p = 1
    c = p*2                 # 왼쪽 자식 번호
    while c <= last:        # 자식이 하나 이상 있으면
        # 오른쪽 자식이 있고, 오른쪽 자식의 키 값이 더 크면
        if c+1 <= last and heap[c] < heap[c+1]:
            c += 1          # 비교 대상을 오른쪽 자식으로 변경
        # 자식이 부모보다 크면
        if heap[c] > heap[p]:
            heap[c], heap[p] = heap[p], heap[c]
            p = c
            c = p*2
        else:
            break
    return tmp

heap = [0] * 101            # 완전 이진 트리 1번 ~ 100번 인덱스 준비
last = 0                    # 완전 이진 트리의 마지막 정점 번호
enq(5)
print(heap[1])
enq(15)
print(heap[1])
enq(8)
print(heap[1])
enq(20)
print(heap[1])

while last > 0:
    print(deq())

'''
output
5
15
15
20
20
15
8
5
'''
```
