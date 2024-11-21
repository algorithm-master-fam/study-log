# Stack, DFS, Backtracking

## 스택(stack)

- 물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 자료구조이다.
- 스택에 저장된 자료는 선형 구조를 갖는다.
    - 선형 구조 : 자료 간 관계가 1대1의 관계를 갖는다.
    - 비선형구조 : 자료 간의 관계가 1대N의 관계를 갖는다.
- 스택에 자료를 삽입하거나 스택에서 자료를 꺼낼 수 있다.
- 마지막에 삽입한 자료를 자료를 가장 먼저 꺼낸다. 후입선출(Last-In-First_Out)이라고 부른다.

## 필요한 자료구조와 연산

- 자료구조 : 자료를 선형으로 저장할 저장소
    - 배열을 사용할 수 있다.
    - 저장소 자체를 스택이라 부르기도 한다.
    - 스택에서 마지막 삽입된 원소의 위치를 `top`이라 부른다.
- 연산
    - 삽입 : 저장소에 자료를 저장한다. 보통 `push`라고 부른다.
    - 삭제 : 저장소에서 자료를 꺼낸다. 꺼낸 자료는 삽입한 자료의 역순으로 꺼낸다. 보통 `pop`이라고 부른다.
    - 스택이 공백인지 아닌지를 확인하는 연산. `isEmpty`
    - 스택의 `top`에 있는 item(원소)를 반환하는 연산. `peek`

## 스택의 push 알고리즘

- `append` 메소드를 통해 리스트의 마지막 데이터를 삽입

```python
def push(item):
    s.append(item)
```

### [참고]

```python
def push(item, size):
    global top
    top += 1
    if top == size:
        print('overflow!')
    else:
        stack[top] = item

size = 10
stack = [0] * size
top -= 1

push(10, size)
top += 1
stack[top] = 20 # push(20)
```

## 스택의 pop 알고리즘

```python
def pop():
    if len(s) == 0:
        # underflow
        return
    else:
        return s.pop()
```

### [참고]

```python
def pop():
    global top
    if top == -1:
        print('underflow!')
        return 0
    else:
        top -= 1
        return stack[top+1]

print(pop())

if top > -1:
    top -= 1
    print(stack[top+1]) # pop()
```

## 스택 구현 : 3개의 데이터 push & pop

```python
stack = [0] * 3
top = -1

# push(10)
top += 1
stack[top] = 10

# push(20)
top += 1
stack[top] = 20

# push(30)
top += 1
stack[top] = 30

if top > -1:
    top -= 1
    print(stack[top+1])

if top > -1:
    top -= 1
    print(stack[top+1])

if top > -1:
    top -= 1
    print(stack[top+1])
```

## 스택의 응용1 : 괄호 검사

- 괄호의 종류 : 대괄호, 중괄호, 소괄호
- 조건
    - 왼쪽 괄호의 개수와 오른쪽 괄호의 개수가 같아야 한다.
    - 같은 괄호에서 왼쪽 괄호는 오른쪽 괄호보다 먼저 나와야 한다.
    - 괄호 사이에는 포함 관계만 존재한다.
- 괄호를 조사하는 알고리즘 개요
    - 문자열에 있는 괄호를 차례대로 조사하면서 **왼쪽 괄호를 만나면 스택에 삽입**하고, **오른쪽 괄호를 만나면 스택에서 top 괄호를 삭제**한 후 **오른쪽 괄호와 짝이 맞는지를 검사**한다.
    - 이 때, 스택이 비어 있으면 조건 1 또는 조건 2에 위배되고 괄호의 짝이 맞지 않으면 조건 3에 위배된다.
    - 마지막 괄호까지를 조사한 후에도 스택에 괄호가 남아 있으면 조건 1에 위배된다.

```
구현해서 추가하기
```

## 스택의 응용2 : function call

- 프로그램에서의 함수 호출과 복귀에 따른 수행 순서를 관리
    - **가장 마지막에 호출된 함수가 가장 먼저 실행을 완료하고 복귀하는 후입선출 구조**이므로, 후입선출 구조의 스택을 이용하여 수행순서 관리
    - 함수 호출이 발생하면 호출한 함수 수행에 필요한 지역변수, 매개변수 및 수행 후 복귀할 주소 등의 정보를 스택 프레임(stack frame)에 저장하여 시스템 스택에 삽입
    - 함수의 실행이 끝나면 시스템 스택의 top 원소(스택 프레임)를 삭제(pop)하면서 프레임에 저장되어 있던 복귀주소를 확인하고 복귀
    - 함수 호출과 복귀에 따라 이 과정을 반복하여 전체 프로그램 수행이 종료되면 시스템 스택은 공백 스택이 된다.

## 재귀 호출

- 자기 자신을 호출하여 순환 수행되는 것
- 함수에서 실행해야 하는 작업의 특성에 따라 일반적인 호출 방식보다 재귀 호출 방식을 사용하여 함수를 만들면 프로그램의 크기를 줄이고 간단하게 작성
    - 재귀 호출의 예) factorial
    - n에 대한 factorial : 1부터 n까지의 모든 자연수를 곱하여 구하는 연산
    - 마지막에 구한 하위 값을 이용하여 상위 값을 구하는 작업을 반복

```
## 피보나치 수열
def fibo(i):
    if i < 2:
        return i
    else:
        return fibo(i-1) + fibo(i-2)

print(fibo(6)) # 피보나치 수열의 index[6] = 8 (0, 1, 1, 2, 3, 5, 8)
```

- 앞의 예에서 피보나치 수를 구하는 함수를 재귀함수로 구현한 알고리즘은 문제점이 있다.
- 엄청난 중복 호출이 존재하기 때문이다.

## Memoization

- 메모이제이션은 컴퓨터 프로그램을 실행할 대 이전에 계산한 값을 메모리에 저장해서 메번 다시 계산하지 않도록 하여 전체적인 실행 속도를 빠르게 하는 기술이다. 동적 계획법의 핵심이 되는 기술이다.
- 앞의 예에서 피보나치 수를 구하는 알고리즘에서 fibo(n)의 값을 계산하자마자 저장하면, 실행시간을 O(n)으로 줄일 수 있다.

```python
# memo를 위한 배열을 할당하고, 모두 0으로 초기화
# memo[0]을 0으로 memo[1]을 1로 초기화

def fibo1(n):
    global memo
    if n >= 2 and memo[n] == 0:
        memo[n] = (fibo1(n-1) + fibo1(n-2))
    return memo[n]

n =
memo = [0] * (n+1)
memo[0] = 0
memo[1] = 1
```

## DP(Dynamic Programming)

- 동적 계획 알고리즘은 그리디 알고리즘과 같이 최적화 문제를 해결하는 알고리즘이다.
- 동적 계획 알고리즘은 먼저 입력 크기가 작은 부분 문제들을 모두 해결한 후에 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결하여, 최종적으로 원래 주어진 입력의 문제를 해결하는 알고리즘이다.
- 피보나치 수 DP 적용 알고리즘

```python
def fibo2(n):
    f = [0] * (n+1)
    f[0] = 0
    f[1] = 1
    for i in range(2, n+1):
        f[i] = f[i-1] + f[i-2]

    return f[n]

print(fibo2(6)) # 8
```

### DP 구현

- recursive 방식 : fibo1()
- iterative : fibo2()
- memoization을 재귀적 구조에 사용하는 것보다 반복적 구조로 DP를 구현한 것이 성능 면에서 보다 효율적이다.
- 재귀적 구조는 내부에 시스템 호줄 스택을 사용하는 오버헤드가 발생하기 때문이다.

```python
def f(i, k):               # i 단계, k 목표
    if i == k:             # 목표에 도달하면
        print(B)
        return
    else:                  # 목표에 도달하지 않은 경우
        B[i] = A[i]
        f(i+1, k)          # 다음 단계로 이동

A = [10, 20, 30]
B = [0] * 3

'''
# 일정 수준 이상 반복되면 에러 발생
A = [i for i in range(1000)]
B = [0] * 1000
f(0, 1000)
# RecursionError: maximum recursion depth exceeded in comparison
'''
```

## Intro

- 비선형구조인 그래프 구조는, 표현된 모든 자료를 빠짐없이 탐색하는 것이 중요
- 아래와 같은 탐색 기법이 존재
    - 깊이 우선 탐색(Depth First Search, DFS)
    - 너비 우선 탐색(Breadth First Search, BFS)

## DFS(Depth First Search, 깊이 우선 탐색)

- 시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하는 순회방법
- 가장 마지막에 만났던 갈림길의 정점으로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 후입선출 구조의 스택 사용

### DFS 알고리즘

1. 시작 정점 v를 결정하여 방문한다.
2. 정점 v에 인접한 정점 중에서

(1) 방문하지 않은 정점 w가 있으면, **정점 v를 스택에 push**하고 정점 w를 방문한다. 그리고 w를 v로 하여 다시 2)를 반복한다.

(2) 방문하지 않은 정점이 없으면, 탐색의 방향을 바꾸기 위해서 스택을 pop하여 받은 가장 마지막 방문 정점을 v로 하여 다시 2)를 반복한다.

1. 스택이 공백이 될 때까지 2)를 반복한다.

```python
# 초기상태 : 배열 visited를 False로 초기화하고, 공백 스택을 생성
visited = [], stack = []
DFS(v)
    visited[v] <- true (시작점 v 방문)
    while {
        if (v의 인접 정점 중 방문 안 한 정점 w가 있으면)
            push(v)
            v <- w (w에 방문)
            visited[w] <- true (중복 방문을 방지하기 위해 표시)
        else (v의 인접 정점 중 방문 안 한 정점 w가 없고)
            if (스택이 비어 있지 않으면)
                v <- pop(stack)
            else (스택이 비어 있으면)
                break
    }
end DFS()
```

가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 계속 반복 탐색하여 모든 정점을 탐색한다.

스택의 후입선출 구조 또는 재귀호출을 통해서 구현하게 된다.

### DFS 연습문제

```python
'''
input
주어진 조건
- 정점, 간선의 수 : 7 8
- 노드 간 연결 관계 : 1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7

output
1 2 4 6 5 7 3
'''

'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

# V(정점), E(간선)
V, E = map(int, input().split())
data = list(map(int, input().split()))

arr = [[0] * (V+1) for _ in range(V+1)] # 정점의 길이보다 + 1
visited = [0] * (V+1)

for i in range(E):
    n1, n2 = data[i*2], data[i*2+1] # 1 2 / 1 3 / 2 4 / 2 5 / 4 6 / 5 6 / 6 7 / 3 7
    arr[n1][n2] = 1 # n1과 n2는 인접했다는 뜻

# 탐색해보기
def dfs(v):
    visited[v] = 1
    print(v, end=' ')

    # 현재 v는 시작 정점!
    # 인접한 정점 중 방문하지 않은 곳
    for w in range(1, V+1):
        if arr[v][w] == 1 and visited[w] == 0:
            dfs(w)

dfs(1)
```

## DFS +

- 그래프를 표현하는 방법 (인접행렬)

```python
# 1. 딕셔너리 활용
graph = {}
graph['A'] = ['B','C']
graph['B'] = ['D','F']

# 2. 2차원 배열 활용
'''
  A B C D E F
A 0 1 1 0 0 0
B 1 0 0 1 0 1
C 1 1 0 1 0 1
D 0 0 1 0 0 0
E 0 0 0 0 0 0
F 0 1 1 0 0 0
'''
```

### DFS 구현 예시

```python
''
7 8 V, E
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

# V(정점), E(간선)
V, E = map(int, input().split())

arr = [[0] * (V+1) for _ in range(V+1)] # 정점의 길이 +1

visited = [0] * (V+1)

for i in range(E):
    n1, n2 = arr[i*2], arr[i*2+1]
    arr[n1][n2] = 1 # n1과 n2는 인접했다는 뜻

## 방법(1)
def dfs(v):
    visited[v] = 1 # 현재 v는 시작 정점!

    for w in range(1, V+1): # 인접한 정점 중 방문하지 않은 곳이 있다면
        if arr[v][w] == 1 and visited[w] == 0:
            dfs(w)

dfs(1)

## 방법(2) 반복문
def dfs(v):
    stack = [v] # stack.append(v)

    while len(stack): # 스택이 빌 때까지 반복
        v = stack.pop()
        visited[v] = 1 # v가 아직 방문 전이라면

        for w in range(1, V + 1):
        if arr[v][w] == 1 visited[w] == 0:
            stack.append(w)

dfs(1)
```

## 계산기

- 문자열로 된 계산식이 주어질 때, 스택을 이용하여 이 계산식의 값을 계산할 수 있다.
- 중위 표기법(infix notaiton) : 연산자를 피연산자의 가운데 표기하는 방법
- 후위 표기법(postfix notation) : 연산자를 피연산자 뒤에 표기하는 방법
- 문자열 수식 계산의 일반적 방법
    - step1. 중위 표기법의 수식을 후위 표기법으로 변경한다 (스택 이용)
        - 수식의 각 연산자에 대해서 우선순위에 따라 괄호를 사용하여 다시 표현한다.
        - 각 연산자를 그에 대응하는 오른쪽 괄호 뒤로 이동시킨다.
        - 괄호를 제거한다.
    - step2. 후위 표기법의 수식을 스택을 이용하여 계산한다.
        - 입력 받은 중위 표기식에서 토큰을 읽는다.
        - 토큰이 피연산이면 토큰을 출력한다.
        - 토큰이 연산자(괄호 포함)일 때, 이 토큰이 스택의 top에 저장되어 있는 연산자보다 우선순위가 높으면 스택에 `push`하고, 그렇지 않으면 스택 `top`의 연산자의 우선순위가 토큰의 우선순위보다 작을 때까지 스택에서 `pop`한 후 토큰의 연산자를 `push`한다. 만약 `top`에 연산자가 없으면 `push`한다.

| **토큰** | **isp** | **icp** |
| --- | --- | --- |
| ) | - | - |
| *, / | 2 | 2 |
| +, - | 1 | 1 |
| ( | 0 | 3 |

```python
icp : in - coming priority
isp : in - stack priority

if (icp > isp):
    push()
else:
    pop()
```

### 계산기 구현 예시 (후위연산)

```python
infix = '(6+5*(2-8)/2)'
stack = []
result = ''

for token in infix:
    # (1) 토큰이 피연산자인 경우
    if token.isdecimal():
        result += token
    # (2) 토큰이 연산자인 경우
    else:
        if not stack: # 스택이 비었다면
            stack.append(token) # push
        else:
        # '('는 icp가 가장 높음
            if token == '(':
                stack.append(token)
            # ')'는 '('가 나오기 전까지 스택에서 pop하고 result에 append
            elif token == ')':
                while stack[-1] != '(':
                    result += stack.pop()
                stack.pop()

            # icp가 2인 경우
            elif token == '*' or token == '/':
                # 스택의 top의 토큰이 우선순위가 낮을 때까지 pop하고 result에 append
                while stack and stack[-1] == '*' or stack[-1] == '/':
                    result += stack.pop()
                stack.append(token)

            # icp가 1인 경우
            elif token == '+' or token == '-':
                # 스택의 top의 토큰이 우선순위가 낮을 때까지 pop하고 result에 append
                # '('가 아닌 경우 모두 동치
                    while stack and stack[-1] != '(':
                        result += stack.pop()
                    stack.append(token)

while stack: # 스택이 텅 비어서 0(False)값이 될 때까지 반복
    result += stack.pop()

print(result) # 6528-*2/+

stack = []

for num in result: # 결과값을 순회
    if num.isdecimal(): # (1) 피연산자인 경우
        stack += num
    else: # (2) 연산자인 경우
        a = int(stack.pop())
        b = int(stack.pop())
        if num == '+':
            stack.append(b+a)
        elif num == '-':
            stack.append(b-a)
        elif num == '*':
            stack.append(b*a)
        elif num == '/':
            stack.append(b/a)

print(*stack)

```

## 백트래킹(Backtracking)

- 해를 찾는 도중에 막히면, 즉 해가 막히면 되돌아가서 다시 해를 찾아가는 기법
- 백트래킹 기법은 최적화 문제와 결정 문제를 해결할 수 있다.
- 결정 문제 : 문제의 조건을 만족하는 해가 존재하는지의 여부를 ‘yes 또는 ‘no’가 답하는 문제
    - 미로 찾기
    - n-Queen 문제
    - Map coloring
    - 부분 집합의 합(Subset Sum) 문제 등

### 백트래킹 vs 깊이우선탐색

- 어떤 노드에서 출하는 경로가 해결책으로 이어질 것 같지 않으면 더 이상 그 경로를 따라가지 않음으로써 시도 횟수를 줄임 (Prunning 가지치기)
- 깊이우선탐색이 모든 경로를 추적하는데 비해 백트랙킹은 불필요한 경로를 조기에 차단
- 깊이우선탐색을 가하기에는 경우의 수가 N!으로 많기 때문에 처리 불가능한 경우 존재
- 백트래킹 역시 최악의 경우 지수함수 시간(Exponential Time)을 요하기 때문에 처리 불가능한 경우 존재

### **백트래킹** 기법

- 어떠 노드의 유망성을 점검한 후에 유망(promising)하지 않다고 결정되면 그 노드의 부모로 되돌아가(backtracking) 다음 자식 노드로 감
- 어떠 노드를 방문하였을 때 그 노드를 포함한 경로가 해답이 될 수 없으면 그 노드는 유망하지 않다고 하며, 반대로 해답의 가능성이 있으면 유망하다고 한다.
- 가지치기(prunning) : 유망하지 않은 노드가 포함되는 경로는 더 이상 고려하지 않는다.

### **백트래킹** 절차

1. 상태 공간 트리의 깊이 우선 검색을 실시
2. 각 노드가 유망한지 점검
3. 만일 그 노드가 유망하지 않으면, 그 노드의 부모 노드로 돌아가서 검색 반복

```python
def checknode(V):
    if promising(v):                        # 유망한 해이면
        if there is a solution at v:        # 최종 해이면
            write the solution              # 해 출력
        else:                               # 최종 해가 아니라면
            for u in each child of v:       # v의 가지를 탐색
                checknode(u)
```

### **백트래킹** 구현 예시

```python
def backtrack(a, k, input):
    global MAXCANDIDATES
    c = [0]*MAXCANDIDATES

    if k == input:
        for i in range(1, k+1):
            print(a[i], end=' ')
        print()
    else:
        k += 1
        ncandidates = construct_candidates(a, k, input, c)
        for i in range(ncandidates):
            a[k] = c[i]
            backtrack(a, k, input)

def construct_candidates(a, k, input, c):
    in_perm = [False] * NMAX

    for i in range(1, k):
        in_perm[a[i]] = True

    ncandidates = 0
    for i in range(1, input+1):
        if in_perm[i] == False:
            c[ncandidates] = i
            ncandidates += 1
    return ncandidates

NMAX = 11
MAXCANDIDATES = 10
a = [0]*NMAX
backtrack(a, 0, 3)
```

# Queue, BFS

## 큐(Queue)

- 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
    - 큐의 뒤에서는 삽입만 하고, 큐의 앞에서는 삭제만 이루어지는 구조
- 선입선출구조(FIFO : First In First Out)
    - 큐에 삽입한 순서대로 원소가 저장되어, 가장 먼저 삽입(First In)된 원소는 가장 먼저 삭제(First Out)된다.

### 큐의 구조 및 기본 연산

- 큐의 선입선출 구조
    - 머리(Front) : 저장된 원소 중 첫번째 원소 (또는 삭제된 위치)
    - 꼬리(Rear) : 저장된 원소 중 마지막 원소
- 큐의 기본 연산
    - 삽입 : `enQueue`
    - 삭제 : `deQueue`
- 큐의 사용을 위해 필요한 주요 연산

| **연산** | **기능** |
| --- | --- |
| `enQueue(item)` | 큐의 뒤쪽(rear 다음)에 원소를 삽입하는 연산 |
| `deQueue()` | 큐의 앞쪽(front)에서 원소를 삭제하고 반환하는 연산 |
| `createQueue()` | 공백 상태의 큐를 생성하는 연산 |
| `isEmpty()` | 큐가 공백 상태인지를 확인하는 연산 |
| `isFull()` |  큐가 포화 상태인지를 확인하는 연산 |
| `Qpeek()` | 큐의 앞쪽(front)에서 원소를 삭제 없이 반환하는 연산 |

### 큐의 연산 과정

| **연산 과정** | **연산** | **변수** | **[0]** | **[1]** | **[2]** | **front** | **rear** | **비고** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1) 공백 큐 생성 | `createQueue()` | front = rear = -1 |  |  |  | -1 | -1 | 초기 상태 |
| 2) 원소 A 삽입 | `enQueue(A)` | rear += 1 | A |  |  | -1 | 0 |  |
| 3) 원소 B 삽입 | `enQueue(B)` | rear += 1 | A | B |  | -1 | 1 |  |
| 4) 원소 반환/삭제 | `deQueue()` | front += 1 |  | B |  | 0 | 1 |  |
| 5) 원소 C 삽입 | `deQueue(C)` | rear += 1 |  | B | C | 0 | 2 |  |
| 6) 원소 반환/삭제 | `deQueue()` | front += 1 |  |  | C | 1 | 2 |  |
| 7) 원소 반환/삭제 | `deQueue()` | front += 1 |  |  |  | 2 | 2 | 공백 상태 |

## 선형 큐

- 1차원 배열을 이용한 큐
    - 큐의 크기 = 배열의 크기
    - front : 저장된 첫번째 원소의 인덱스 (= 마지막으로 dequeue된 원소의 인덱스)
    - rear : 저장된 마지막 원소의 인덱스
- 상태 표현
    - 초기 상태 : front == rear == -1
    - 공백 상태 : front == rear
    - 포화 상태 : rear == n-1 (n : 배열의 크기, n-1 : 배열의 마지막 인덱스)

### 선형 큐 구현

- 초기 공백 큐 생성
    - 크기 n인 1차원 배열 생성
    - front와 rear를 -1로 초기화

#### 삽입 : `enQueue(item)`

- 마지막 원소 뒤에 새로운 원소를 삽입하기 위해
    - rear 값을 하나 증가시켜 새로운 원소를 삽입할 자리를 마련
    - 그 인덱스에 해당하는 배열 원소 Q[rear]에 item을 저장

```python
def enQueue(item):
    global rear
    if isFull(): # 포화 상태가 되어 더 이상 원소를 저장할 수 없는 경우
        print('Queue_Full)
    else:
        rear <- rear + 1
        Q[rear] <- item
```

#### 삭제 : `deQueue()`

- 가장 앞에 있는 원소를 삭제하기 위해
    - front 값을 하나 증가시켜 큐에 남아있게 될 첫번째 원소 이동
    - 새로운 첫번째 원소를 리턴 함으로써 삭제와 동일한 기능

```python
deQueue():
    if(isEmpty()) then Queue_Empty()
    else:
        front <- front + 1
        return Q[front]
```

#### 공백 상태 및 포화 상태 검사 : `isEmpty()`, `isFull()`

- 공백 상태 : front == rear
- 포화 상태 : rear == n-1 (n : 배열의 크기, n-1 : 배열의 마지막 인덱스)

```python
def isEmpty():
    return front == rear

def isFull():
    return rear == len(Q) - 1
```

#### 검색 : `Qpeek()`

- 가장 앞에 있는 원소를 검색하여 반환하는 연산
- 현재 front의 한자리 뒤(front+1)에 있는 원소, 즉 큐의 첫번째에 있는 원소를 반환

```python
def Qpeek():
    if isEmpty():
        print('Queue_Empty')
    else:
        return Q[front+1]
```

### 큐 구현 예시

```python
## ▼ (1) 함수 구현
def enqueue(data):
    global rear
    rear += 1
    queue[rear] = data

def dequeue():
    global front
    front += 1
    return queue[front]

queue = [0]*10
front = -1
rear = -1

rear += 1
queue[rear] = 1

enqueue(2)
enqueue(3)

if front != rear: # 1 출력
    print(dequeue())

if front != rear: # 2 출력
    print(dequeue())

if front != rear: # 3 출력
    print(dequeue())

if front != rear: # 출력 X
    print(dequeue())

## ▼ (2) 지양해야 할 형태 (사이즈가 크고, 반복 횟수가 많은 경우 시간 초과)
q = []
q.append(10)
q.append(20)
q.append(30)
print(q.pop(0)) # 10
print(q.pop(0)) # 20
print(q.pop(0)) # 30

## ▼ (3) 라이브러리 사용 (속도 빠름, but 제약 상황을 대비하여 (1) 방식 연습)
from collections import deque
q1 = deque()
q1.append(100)
q1.append(200)
q1.append(300)
print(q1.popleft()) # 100
print(q1.popleft()) # 200
print(q1.popleft()) # 300
```

### 선형 큐 이용시의 문제점

- 잘못된 포화상태 인식
    
    선형 큐를 이용하여 원소의 삽입과 삭제를 계속할 경우, 배열의 앞부분에 활용할 수 있는 공간이 있음에도 불구하고, rear=n-1인 상태 즉, 포화상태로 인식하여 더 이상의 삽입을 수행하지 않게 됨 (아래 표와 같은 상황을 포화 상태로 잘못 인식)
    

| [0] Null | [1] Null | [2] Null | [3] front | [4] rear |
| --- | --- | --- | --- | --- |
- 해결 방법 (1)
    - ~~매 연산이 이루어질 때마다 저장된 원소들을 배열의 앞부분으로 모두 이동시킴~~
    - 원소 이동에 많은 시간이 소요되어 큐의 효율성이 급격히 떨어짐
- 해결 방법 (2)
    - 1차원 배열을 사용하되, 논리적으로는 배열의 처음과 끝이 연결되어 원형 형태의 큐를 이룬다고 가정하고 사용
    - **원형 큐**의 논리적 구조

## 원형 큐의 구조

- 초기 공백 상태
    - front = rear = 0
- Index의 순환
    - front와 rear의 위치가 배열의 마지막 인덱스인 n-1를 가리킨 후, 그 다음에는 논리적 순환을 이루어 배열의 처음 인덱스인 0으로 이동해야 함
    - 이를 위해 나머지 연산자 `mod`를 사용함
- front 변수
    - 공백 상태와 포화 상태 구분을 쉽게 하기 위해 **front가 있는 자리는 사용하지 않고 항상 빈자리로 둠**
- 삽입 위치 및 삭제 위치

|  | **삽입 위치** | **삭제 위치** |
| --- | --- | --- |
| **선형 큐** | rear = rear + 1 | front = front + 1 |
| **원형 큐** | rear = (rear + 1) mod n | front = (front + 1) mod n |

### 원형 큐 구현

- 초기 공백 큐 생성
    - 크기 n인 1차원 배열 생성
    - front와 rear를 0으로 초기화

#### 공백 상태 및 포화 상태 검사 : `isEmpty()`, `isFull()`

- 공백 상태 : front == rear
- 포화 상태 : 삽입할 rear의 다음 위치 == 현재 front
- (rear + 1) mod n == front

```python
def isEmpty():
    return front == rear

def isFull():
    return (rear+1) % len(cQ) == front
```

#### 삽입 : `enQueue(item)`

- 마지막 원소 뒤에 새로운 원소를 삽입하기 위해
    - rear 값을 조정하여 새로운 원소를 삽입할 자리를 마련함
    - rear ← (rear + 1) mod n
    - 그 인덱스에 해당하는 배열 원소 cQ[rear]에 item을 저장

```python
def enQueue(item):
    global rear
    if isFull():
        print('Queue_Full')
    else:
        rear = (rear+1) % len(cQ)
        cQ[rear] = item
```

#### 삭제 : `deQueue()`, `delete()`

- 가장 앞에 있는 원소를 삭제하기 위해
    - front 값을 조정하여 삭제할 자리를 준비
    - 새로운 front 원소를 리턴 함으로써 삭제와 동일한 기능

```python
def deQueue():
    global front
    if isEmpty():
        print('Queue_Empty')
    else:
        front = (front+1) % len(cQ)
        return cQ[front]
```

## 우선순위 큐

- 우선순위를 가진 항목들을 저장하는 큐
- FIFO 순서가 아니라 우선순위가 높은 순서대로 먼저 나가게 된다.
- 적용 분야
    - 시뮬레이션 시스템, 네트워크 트래픽 제어, 운영체제의 테스크 스케줄링

### 우선순위 큐의 구현

- 배열을 이용한 우선순위 큐
- 리스트를 이용한 우선순위 큐
- 기본 연산
    - 삽입 : `enQueue`
    - 삭제 : `deQueue`

## 큐의 활용 : 버퍼(Buffer)

- 버퍼
    - 데이터를 한 곳에 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리의 영역
    - 버퍼링 : 버퍼를 활용하는 방식 도는 버퍼를 채우는 동작을 의미
- 버퍼의 자료 구조
    - 버퍼는 일반적으로 입출력 및 네트워크와 관련된 기능에서 이용된다.
    - 순서대로 입력/출력/전달되어야 하므로 FIFO 방식의 자료구조인 큐가 활용된다.

## ⭐ BFS(Breadth First Search, 너비 우선 탐색)

- 너비 우선 탐색은 탐색 시작점의 인접한 정점들을 모두 차례로 방문한 후에, 방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문하는 방식
- 인접한 정점들에 대해 탐색을 한 후, 차례로 다시 너비우선탐색을 진행해야 하므로, 선입선출 형태의 자료구조인 큐를 활용한다.

### BFS 알고리즘

```python
def BFS(G, v):                          # 그래프 G, 탐색 시작점 v
    visited = [0]*(n+1)                 # 중복 방문 방지용, n : 정점의 개수
    queue = []                          # 큐 생성
    queue.append(v)                     # 시작점 v를 큐에 삽입
    while queue:                        # 큐가 비어있지 않은 경우
        t = queue.pop(0)                # 큐의 첫번째 원소 반환
        if not visited[t]:              # 방문되지 않은 곳이라면
            visited[t] = True           # 방문한 것으로 표시
            visited(t)                  # 정점 t에서 할 일
            for i in G[t]:              # t와 연결된 모든 정점에 대해
                if not visited[i]:      # 방문되지 않은 곳이라면
                    queue.append(i)     # 큐에 넣기
```

### [참고] BFS 예제

```python
def BFS(G, v, n):                             # 그래프 G, 탐색 시작점 v
    visited = [0]*(n+1)                       # 중복 방문 방지용, n : 정점의 개수
    queue = []                                # 큐 생성
    queue.append(v)                           # 시작점 v를 큐에 삽입
    **visited[v] = 1                            # 시작점이 enqueue 되었음을 표시**
    while queue:                              # 큐가 비어있지 않은 경우
        t = queue.pop(0)                      # 큐의 첫번째 원소 반환
        visit(t)
        for i in G[t]:                        # t와 연결된 모든 정점에 대해
            if not visited[i]:                # 방문되지 않은 곳이라면
                queue.append(i)               # 큐에 넣기
                visited[i] = visited[n] + 1   # n으로부터 1만큼 이동
```
