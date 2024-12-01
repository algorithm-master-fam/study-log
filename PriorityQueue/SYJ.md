# 우선순위 큐 
우선순위 큐 란 데이터를 추가(put)한 순서와 상관없이, 데이터를 꺼낼 때(get) 값을 오름차순하여 반환하는 특징을 갖고 있는 자료구조이다.
- 데이터를 삽입할 때마다 큐에 있는 데이터를 하나씩 비교해서 우선순위에 맞는 자리를 찾아 넣어야 하므로 
  최악의 경울 데이터가 N개일 경우, O(N)의 시간복잡도를 가진다.
  이런 점을 보완하기 위해 우선순위 큐를 구현할 때는 힙 자료구조를 사용한다.
  우선 순위 큐 내부에는 데이터를 정렬된 상태로 보관하는 로직이 있으며 heapq 모듈을 통해 구현되어 있다.
  우선순위 큐의 put(), get() 메서드는 O(logn)의 시간 복잡도를 가진다.

# 힙
힙은 기본적으로 완전 이진트리로 되어있다.
모든 노드의 우선순위가 자식 노드의 우선순위보다 크거나 같으며,
우선순위의 기준에 따라 최대 힙과 최소힙으로 나뉜다.

## 최대 힙
![image](https://github.com/user-attachments/assets/20f10679-a9c1-49fe-a551-b84d82b36716)
값이 클수록 우선순위가 높다.
부모노드 >= 자식노드
## 최소 힙
![image](https://github.com/user-attachments/assets/b01f56f6-8667-488f-82ab-1ce9ee83e534)
값이 작을수록 우선순위가 높다.
부모노드 <= 자식노드

## Priority Queue VS heqpq
Priority Queue는 Thread Safe하고 Heapq는 Non Safe하다. 
코딩테스트에서 우선순위큐 문제를 만나면 속도가 더 빠른 Heapq를 사용하자.

# 파이썬에서의 우선순위 큐(heqpq) 사용법
## heapq.heappush(heap, item)
최소힙 자료구조 특성을 유지.
item값을 heap에 추가하는 메서드.
가장 작은 값이 heap[0]에 위치하게 됨.
``` python
import heapq

num_list = [3,1,2,7,5]
result = []
for num in num_list :
  heapq.heappush(result, num)
```

## heapq.heappop(heap)
최소힙 자료구조 특성 유지.
heap의 첫번째 요소를 삭제 후 반환하는 메서드.
``` python
for _ in range(len(result)):
  print(heapq.heappop(result))
```

## heapq.heapify(list)
기존에 존재하는 리스트를 받아 Heap 구조로 변환하는 메서드
``` python
heapq.heapify(nun_list)
```

## 최대힙 구현
각 값들에 - 를 붙이고 heap에 넣은 뒤, heappop한 값에 다시 -를 붙여주면 된다.
``` python
import heapq

num_list = [1,2,3,4,5]
heap = []
max_heap = []

for num in num_list:
  heapq.heappush(heap,-num)
print(heap)

for i in range(len(heap)):
  max_heap.append(-heapq.heappop(heap))
print(max_heap)
```

### References
https://www.daleseo.com/python-priority-queue/
https://login-data.tistory.com/28
