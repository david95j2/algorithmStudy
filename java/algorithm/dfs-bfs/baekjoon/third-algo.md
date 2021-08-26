# 그래프 탐색 알고리즘 : DFS/BFS

---
- 탐색이란 많은 양의 데이터 중에서 **원하는 데이터를 찾는 과정**을 말한다.
- 대표적인 그래프 탐색 알고리즘으로는 DFS와 BFS가 있다.


### 스택 자료구조

- 먼저 들어 온 데이터가 나중에 나가는 형식(선입후출)의 자료구조이다.
- 입구와 출구가 동일한 형태로 스택을 시각화할 수 있다.

```java
public static void main(String[] args) {
    	
    	Stack<Integer> s = new Stack<>();
    	
    	s.push(5);
    	s.push(2);
    	s.push(3);
    	s.push(7);
    	s.pop();
    	s.push(1);
    	s.push(4);
    	s.pop();
    	
    	while (!s.empty()) {
    	    System.out.print(s.peek() + " ");
    	    s.pop();
    	}
}
```

### 큐 자료구조

- 먼저 들어 온 데이터가 먼저 나가는 형식(선입선출)의 자료구조이다.
- 큐는 입구와 출구가 모두 뚫려 있는 터널과 같은 형태로 시각화 할 수 있다.

```java
public static void main(String[] args) {
    	
    	Queue<Integer> q = new LinkedList<>();
    	
    	q.offer(5);
    	q.offer(2);
    	q.offer(3);
    	q.offer(7);
    	q.poll();
    	q.offer(1);
    	q.offer(4);
    	q.poll();
    	
    	while (!q.empty()) {
    	    System.out.print(q.poll() + " ");
    	}
}
```