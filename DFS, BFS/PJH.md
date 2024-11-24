## Stack & Queue 
> : 스택과 큐는 임시데이터를 처리하되, 데이터를 처리하는 순서에 중점을 둔 자료구조


### Stack
> : '쌓다'라는 의미를 가지고 있듯, 데이터를 쌓는 자료 구조 
> 

---

#### Stack의 3가지 제약 
1. 데이터는 스택의 끝에만 삽입 가능
2. 데이터는 스택의 끝에서만 삭제 가능
3. 스택의 마지막 원소만 읽기 가능   
   ⇒ 이러한 제약을 정리하면 스택은 먼저 들어간 자료가 나중에 나오는 “**LIFO(Last In, Fisrt Out) 후입선출**” 방식  
   ⇒ 스택의 끝을 위(=top), 시작을 끝(=bottom)라고 부른다. 

---

#### Stack 연산 
1. 원소 삽입 = `push()` 
    ```java
    Stack<Integer> stack = new Stack<>(); // int형 스택 선언
    
    stack.push(2);
    stack.push(6);
    stack.push(9);
    stack.push(3);
    
    System.out.println(stack); // 출력 결과 [2, 6, 9, 3]  
    ```

2. 원소 제거 = `pop()`
    ```java
    Stack<Integer> stack = new Stack<>(); // int형 스택 선언
    
    stack.push(2);
    stack.push(6);
    stack.push(9);
    stack.push(3);
    
    stack.pop(); //가장 위에 있는(top) 원소 제거
    
    System.out.println(stack); // 출력 결과 [2, 6, 9]
    ```

3. 모든 원소 제거 = `clear()`
    ```java
    Stack<Integer> stack = new Stack<>(); // int형 스택 선언
    
    stack.push(2);
    stack.push(6);
    stack.push(9);
    stack.push(3);
    
    stack.clear();
    
    System.out.println(stack); // 출력 결과 []
    ```

4. 스택 내 가장 상단 원소 값 반환 = `peek()`
    ```java
    Stack<Integer> stack = new Stack<>(); // int형 스택 선언
    
    stack.push(2);
    stack.push(6);
    stack.push(9);
    stack.push(3);
    
    System.out.println(stack.peek()); //출력 결과 6
    ```

5. 기타 메서드 
    ```java
    Stack<Integer> stack = new Stack<>(); // int형 스택 선언
    
    stack.push(2);
    stack.push(6);
    stack.push(9);
    stack.push(3);
    
    System.out.println(stack.size()); //출력결과 4
    System.out.println(stack.isEmpty()); //출력결과 false
    System.out.println(stack.contains(6)); //출력결과 true
    
    /*
    size() : 스택 크키 리턴
    isEmpty() : 스택이 비었다면 true, 비어있지 않다면 false 리턴
    contains(value) : 스택이 "value"를 포함한다면 true, 포함하고 있지 않다면 false 리턴
    */
    ```

---

#### 추상 데이터 타입(Abstract Data Type, ADT)  

- 추상 데이터 타입(ADT)
    > 구현하고자 하는 구조에 대해 구현 방법은 명시하지 않고 자료구조의 특성들과 어떤 Operations들이 있는지 설명하는 자료구조의 형태  
     = 규칙들의 나열  
  > 
  > e.g. Stack, Queue, 집합
- 대부분의 프로그래밍 언어에는 스택, 큐가 내장 데이터 타입이나 클래스로 딸려 있지 않다  
  → 구현은 사용자의 몫  
- 일반적으로 스택을 생성하려면 실제로 데이터를 저장할 내장 데이터 구조 중 하나를 골라야 한다

    
  <details>
  <summary>ADT(Abstract Data Type) vs DS(Data Structure)  </summary>
  <div markdown="1">

    - interface → ADT 
    - class → DS   
    - 자바의 인터페이스는 ADT라고 할 수 있으며, 이를 실제로 구현하는 class를 DS로 볼 수 있다.   
    - 실제로 스택과 큐가 어떻게 구현하는 것인지가 추가되면 이는 DS로써 스택과 큐를 설명하는 것.  
  </div>
  </details>

---
### Queue
> : '무엇을 기다리다'라는 의미를 가지고 있듯, 줄을 지어 순서대로 처리되는 자료구조 
> 
> 

#### Queue의 3가지 제약 
1. 데이터는 큐의 끝에만 삽입 가능
2. 데이터는 큐의 앞에서만 삭제 가능
3. 큐의 앞에 있는 원소만 읽기 가능  
   ⇒ 이러한 제약을 정리하면 큐는 데이터를 일시적으로 쌓아두기 위한 Stack과 달리 **FIFO 형태**  
   ⇒ 먼저 들어온 데이터가 가장 먼저 나가는 구조로, 큐에 첫 번째로 추가된 항목이 가장 먼저 제거됨  
   ⇒ 큐의 시작을 앞(=front), 끝을 뒤(=back)라고 부름 


--- 

#### Queue 연산 
1. 원소 삽입 = `offer() || add()` 
    ```java
    //java에서 Queue 생성을 위해선 LikendList 활용하여 생성 필수
    Queue<Integer> q = new LinkedList<>(); // int형 queue 선언
    
    q.offer(2);
    q.offer(6);
    q.offer(9);
    q.offer(3);
    
    System.out.println(q); // 출력 결과 : [2, 6, 9, 3]
    ```
   
2. 원소 제거 = `poll()`  
    ```java
    //java에서 Queue 생성을 위해선 LikendList 활용하여 생성 필수
    Queue<Integer> q = new LinkedList<>(); // int형 queue 선언
    
    q.offer(2);
    q.offer(6);
    q.offer(9);
    q.offer(3);
    
    q.poll();
    
    System.out.println(q); // 출력 결과 : [6, 9, 3]
    ```

3. 모든 원소 제거 = `clear()`
    ```java
    //java에서 Queue 생성을 위해선 LikendList 활용하여 생성 필수
    Queue<Integer> q = new LinkedList<>(); // int형 queue 선언
    
    q.offer(2);
    q.offer(6);
    q.offer(9);
    q.offer(3);
    
    q.clear();
    
    System.out.println(q); // 출력 결과 : []
    ```

4. 가장 상단 값 반환 = `peek()`
    ```java
    //java에서 Queue 생성을 위해선 LikendList 활용하여 생성 필수
    Queue<Integer> q = new LinkedList<>(); // int형 queue 선언
    
    q.offer(2);
    q.offer(6);
    q.offer(9);
    q.offer(3);
    
    System.out.println(q.peek()); // 출력 결과 : 2
    
    /*
    poll() 또한 같은 값(2)을 리턴한다.
    하지만 peek()은 값 리턴 후 원소를 삭제하지 않고 단지 확인만 하는 메서드
    */
    ```
5. 기타 연산 
      <details>
      <summary>enqueue/dequeue/peek </summary>
      <div markdown="1">
    
     ![스크린샷 2024-11-24 오후 10.58.22.png](..%2F..%2F..%2F..%2F..%2F..%2Fvar%2Ffolders%2Fph%2F_z8zjw6x6bggjw1q_n4bv4x80000gn%2FT%2FTemporaryItems%2FNSIRD_screencaptureui_mgaRbg%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202024-11-24%20%EC%98%A4%ED%9B%84%2010.58.22.png)
      </div>
      </details>

---

### Stack과 Queue 정리
> 1. Stack   
> - 스택은 같은 크기의 자료를 정해진 한 방향으로만 입력/저장/삭제 가능
> - LIFO 구조이기에 가장 마지막에 들어온 데이터가 가장 먼저 리턴 
> - 주로 실행 취소, 후위 표기법 계산 문제에 적용 가능 
> 2. Queue 
> - 큐는 양방향의 입구로 한쪽은 데이터의 입력을, 다른 쪽에선 데이터의 출력이 이루어짐 
> - 먼저 입력된 데이터를 가르키는 = front = dequeue() 삭제 연산만 수행
> - 가장 마지막에 들어온 데이터를 가르키는 = rear = enqueue() 삽입 연산만 수행
> - 주로 프로세스 관리, 캐시, 너비 우선 탐색 문제 등에 적용 가능 

---

## BFS & DFS 

> **_BFS(Breadth-First Search, 너비 우선 탐색)_**   
> : 한 우물 파기 = 두 지점 사이 최단 경로 찾기 문제 = 재귀/Stack   
> 
> _**DFS(Depth-First Search, 깊이 우선 탐색)**_  
> : 같은 층에 있는 정점들 함께 탐색 = 모든 경우의 수 탐색(미로 문제) = Queue 
> 

---

### DFS(Depth-First Search) : 깊이 우선 탐색   

- 자기 자신을 호출하는 순환 알고리즘 형태 = 재귀 함수 & Stack 자료구조 사용해 해결 가능 
- 그래프 탐색 시, 무한 루프에 빠지지 않기 위해 노드 방문 여부 표시 필수 
- 최대한 멀리 있는 노드 우선 탐색
- 모든 노드를 방문하고자 할 때 사용하기 좋음 
- 속도면에선 BFS보다 느린 단점 존재 
- O(N^2) = 깊게 탐색
```java
static void dfs(int n) {
    V[n] = true; //현재 노드 방문 처리
    sb.append((n+1)+" ");
  
    for(int e: G.get(n)) //인접 노드 탐색
        if(V[e]==false) //방문하지 않은 인접 노드들 중 가장 작은 노드 스택에 넣음
           dfs(e); 
}
```

---

### BFS(Breadth-First Search) : 너비 우선 탐색 

- 재귀적으로 동작하지 않음
- 그래프 탐색 시, 무한 루프에 빠지지 않기 위해 노드 방문 여부 표시 필수
- 방문한 노드를 저장시킨 후 꺼내기 위해 Queue 자료구조 사용(=FIFO)해 해결 가능 
  - C++ : queue(stl)
  - Java : Queue
  - Python : collections.deque() 활용 
  - 인접한 노드를 반복적으로 큐에 넣는다면, 먼저 들어온 요소가 먼저 나가게 되고, 즉 가까운 노드부터 탐색 가능 
- 시작 노드로부터 가장 가까운 노드들을 먼저 방문 탐색
- 두 노드 사이 최단 경로 or 특정 경로 찾고 싶을 때 사용하기 좋음 
- O(N^2) = 넓게 탐색   
```java
static void bfs(int n) {
    int[] q = new int[1000];
    int front = 0; int rear = 0;
    V[n] = true; //현재 노드 방문 처리 
    q[rear++] = n;
    
    while(front != rear) { //큐 빌때까지 반복 
        n = q[front++];
        sb.append((n+1)+" ");
        
        for(int e: G.get(n)) { //인접한 노드 중 아직 방문하지 않은 원소들을 큐에 삽입
            if(V[e]==false){
                V[e]=true;
                q[rear++]=e;
            }
        }
    }
}
```
