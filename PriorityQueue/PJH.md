## Priority Queue
> : 일반적인 큐의 FIFO 처리 방식을 가지며, 우선순위가 높은 데이터가 먼저 나가는 자료구조 
> 
> 

---

### Priority Queue란?
우선순위 큐를 사용하기 위해선 아래와 같은 방법이 필요한데, 
> 1. Comparable Interface를 통해 우선순위 큐에 저장할 객체 구현  
> 2. 자연스레, `compareTo()`를 override해야 되며, 각 객체에서 처리할 우선순위 조건을 리턴
> 3. Priority Queue에서 스스로 우선순위가 높은 객체 추출

Priority Queue 구현은 Heap을 이용해 구현하는 것이 일반적이다.  
  
- 최대값이 우선순위인 큐 = 최대 힙
- 최소값이 우선순위인 큐 = 최소 힙

---

### Priority Queue 특징
1. 삭제와 접근에 있어 전형적인 큐와 비슷하나 삽입에 있어 정렬된 배열과 비슷한 리스트
2. 높은 우선순위의 요소를 먼저 꺼내 처리하는 구조 = **`비교할 수 있는 조건이 존재해야 함`** 
3. 내부 요소는 힙으로 구성되어 이진트리 구조를 갖춰야 함 
4. 내부 구조가 힙으로 구성되어 있으므로 O(NlogN)의 시간복잡도를 가짐 
5. 우선순위를 중요시해야 하는 경우 사용하기에 적합

---


## Heap
> - 힙이란?   
> : 최솟값 또는 최대값을 빠르게 찾아내기 위해 완전이진트리 형태로 만들어진 자료구조  
> - 이진 힙이란?    
> : 특수한 종류의 이진 트리  
> => 즉, 각 노드에 최대 자식 노드가 둘인 트리를 의미
>
### 이진 힙 조건  
이진 힙은 각 노드의 값은 그 노드의 모든 자식 노드의 값보다 커야 하는 조건을 가지고 있으며, 이때의 규칙을 힙 조건(heap condition)이라 부른다.  

아래 예시 그림을 보면, 각 노드는 그 자식보다 크므로 힙 조건을 만족하고 있다.  
![스크린샷 2024-12-01 오후 10.44.43.png](..%2F..%2F..%2F..%2F..%2F..%2Fvar%2Ffolders%2Fph%2F_z8zjw6x6bggjw1q_n4bv4x80000gn%2FT%2FTemporaryItems%2FNSIRD_screencaptureui_nFi1WK%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202024-12-01%20%EC%98%A4%ED%9B%84%2010.44.43.png)
이진 탐색 트리가 떠오를 수 있는데,  
이진 탐색 트리에서 각 노드의 오른쪽 자식은 그 노드보다 크지만 힙에서의 노드는 그 노드의 모든 자식보다 크다는 점을 볼 수 있다.  

### 완전 트리  
- 완전 트리란 빠진 노드 없이 모든 노드가 완전히 채워진 트리를 의미
- 트리의 각 레벨을 왼쪽 -> 오른쪽으로 읽었을 때 모든 자리마다 노드가 존재해야 함 
- 맨 하위 라인에 노드가 빌 순 있으나, 빈 자리의 오른쪽으로 어떠한 노드도 없어야 함  

---

### Priority Queue 우선순위 부여 조건  
1. `java.lang.Comparable` : **원소 스스로** 다른 원소와 자신을 비교할 때 사용하는 방법
    - compareTo() 구현 필요
    - 자기 자신과 매개변수 객체 비교 
2. `java.util.Comparator` : 두 개의 원소 대소 비교를 **비교자가 판단**하는 방법 
    - compare() 구현 필요
    - 두 매개변수 객체 비교 

---


### Priority Queue - Comparable 
> 자기 자신과 매개변수 객체 비교 

- int compareTo(T other) : 비교, 판단 결과를 int형으로 반환
- 자기 자신 - other 
  - 음수 : A > B, A가 더 작을 경우
  - 양수 : A < B, B가 더 클 경우
  - 0 : A = B, 두 원소가 같을 경우 

```java
public class PriorityQueue implements Comparable<Type> {

    @Override
    public int compareTo(Type o) {
        // TO-DO
    }
}
```

```java
public class User implements Comparable<User> {
    String name;
    int age;

    User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(User o) {
        // 1. 유저 이름으로 정렬 
        int result = this.name.compareTo(o.name);
        // 2. 만약 같을 경우, 나이순 정렬 
        if(result == 0) {
            res = this.age - o.age;
        }
        
        return result;
    }
}
```

---
### Priority Queue - Comparator
> 두 매개변수 객체 비교 

- int compareTo(T o1, T o2) : 비교, 판단 결과를 int형으로 반환
- o1 - o2
    - 음수 : o1 < o2, o1이 더 작은 경우(=오름차순)
    - 양수 : o1 > o2, o1이 더 큰 경우(=내림차순)


```java
// 클래스 사용의 경우 
public static class PriorityQueue implements Comparator<Type> {
    @Override
    public int compare(Type o1, Type o2) {
        return o1 - o2;
    }
}

// Priority Queue 사용의 경우
    PriorityQueue<Integer> queue = new PriorityQueue<Integer>(new Comparator<Integer>() {
        @Override
        public int compare(Integer o1, Integer o2) {
            return o1 - o2;
        }
    });
```

```java
PriorityQueue<User> queue = new PriorityQueue<User>(new Comparator<User>() {
    @Override
    public int compare(User o1, User o2) {
        //1. 유저 이름으로 정렬 
        int result = o1.name - o2.name;
        //2. 같을 경우 나이 정렬 
        if(result == 0) {
            result = o1.age - o2.age;
        }
        return result;
        }
    });
```

두 방법으로 우선순위 큐 구현이 가능한데, 어떤 방법이 좋을까?  
- 직접 만든 클래스를 비교 기준으로 삼고 싶다면 Comparable 사용을 추천
- 하지만, 이미 비교 기준이 있는 Integer, String, Character 등의 기준을 바꾸고 싶다면 Comparator 확장해 사용하기  
