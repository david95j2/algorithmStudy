# 그래프 탐색 알고리즘 : DFS/BFS

---
- 탐색이란 많은 양의 데이터 중에서 **원하는 데이터를 찾는 과정**을 말한다.
- 대표적인 그래프 탐색 알고리즘으로는 DFS와 BFS가 있다.

---
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
---
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
---
### 재귀 함수

- 재귀 함수(Recursive Function)란 자기 자신을 다시 호출하는 함수를 의미한다.
- 단순한 형태의 재귀함수 예제

> '재귀 함수를 호출한다.' 라는 문자열을 무한히 출력한다.
>
> 어느 정도 출력하다가 최대 재귀 깊이 초과 메세지가 출력된다.

---

### DFS(Depth-First Search) 

- DFS는 깊이 우선 탐색이라고도 부르며 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘이다.
- DFS는 스택 자료구조(혹은 재귀 함수)를 이용하며, 구체적인 동작 과정은 다음과 같다.

    - 탐색 시작 노드를 선택하고 스택에 삽입하고 방문처리를 한다.
    - 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문처리한다.
    - 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
    - 더 이상 2~3번의 과정을 수행할 수 없을 때까지 반복한다.
  
---
### BFS(Breadth-First Search) 

- BFS 는 너비 우선 탐색이라고도 부르며, 그래프에서 가까운 노드부터 우선적으로 탐색하는 알고리즘 이다.
- BFS 는 큐 자료구조를 이용하며, 구체적인 동작 과정은 다음과 같다.

    - 탐색 시작 노드를 큐에 삽입하고 방문처리를 한다.
    - 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문처리한다.
    - 더이상 2번의 과정을 수행할 수 없을 때까지 반복한다.
    
    - BFS는 시작 정점으로부터 거리가 가까운 정점의 순서로 탐색한다. (거리 1부터 2, 3 순서대로)
    - 그래프 탐색의 경우 어떤 노드를 방문했었는지 여부를 반드시 검사해야 한다. (이를 검사하지 않을 경우 무한루프에 빠질 위험이 있다.)
    - BFS는 재귀적으로 동작하지 않는다.
    - BFS는 방문한 노드들을 차례로 저장한 후 꺼낼 수 있는 자료 구조인 큐(Queue)를 사용한다.
    - 즉, 선입선출(FIFO) 원칙으로 탐색
    - 일반적으로 큐를 이용해서 반복적 형태로 구현하는 것이 가장 잘 동작한다.

구현해보도록 하자
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQ02IX%2FbtqNJv5vkjp%2FgXc4bR2U9NmKpFE6ckIjDK%2Fimg.png)

1. a 노드(시작 노드)를 방문한다. (방문한 노드 체크) 

- 큐에 방문된 노드를 삽입(enqueue)한다.
  
- 초기 상태의 큐에는 시작 노드만이 저장

2. 큐에서 꺼낸 노드과 인접한 노드들을 큐에 추가한다. (모두 차례로 방문)
큐에서 꺼낸 노드를 방문한다.

- 큐에서 꺼낸 노드과 인접한 노드들을 모두 방문한다.

- 인접한 노드가 없다면 큐의 앞에서 노드를 꺼낸다(dequeue).

- 큐에 방문된 노드를 삽입(enqueue)한다.

3. 큐가 공백 상태가 될 때까지 계속한다.


```java
LinkedList<Integer>[] adjList = new LinkedList[n + 1];

for (int i = 0; i <= n; i++) {
	adjList[i] = new LinkedList<Integer>();
}

// 두 정점 사이에 여러 개의 간선이 있을 수 있다.
// 입력으로 주어지는 간선은 양방향이다.
for (int i = 0; i < m; i++) {
	int v1 = sc.nextInt();
	int v2 = sc.nextInt();
	adjList[v1].add(v2);
	adjList[v2].add(v1);
}

for (int i = 1; i <= n; i++) { 
	Collections.sort(adjList[i]); // 방문 순서를 위해 오름차순 정렬 
}

System.out.println("BFS - 인접리스트");
bfs_list(v, adjList, visited);

```


```java
import java.util.*;

public class BFS_Array {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		int n = sc.nextInt(); // 정점의 개수 
		int m = sc.nextInt(); // 간선의 개수 
		int v = sc.nextInt(); // 탐색을 시작할 정점의 번호 

		boolean visited[] = new boolean[n + 1]; // 방문 여부를 검사할 배열 

		int[][] adjArray = new int[n+1][n+1];

		// 두 정점 사이에 여러 개의 간선이 있을 수 있다.
		// 입력으로 주어지는 간선은 양방향이다.
		for(int i = 0; i < m; i++) {
			int v1 = sc.nextInt();
			int v2 = sc.nextInt();

			adjArray[v1][v2] = 1;
			adjArray[v2][v1] = 1;
		}

		System.out.println("BFS - 인접행렬");
		bfs_array(v, adjArray, visited);
	}
	
	// BFS - 인접행렬
	public static void bfs_array(int v, int[][] adjArray, boolean[] visited) {
		Queue<Integer> q = new LinkedList<>();
		int n = adjArray.length - 1;

		q.add(v);
		visited[v] = true;

		while (!q.isEmpty()) {
			v = q.poll();
			System.out.print(v + " ");

			for (int i = 1; i <= n; i++) {
				if (adjArray[v][i] == 1 && !visited[i]) {
					q.add(i);
					visited[i] = true;
				}
			}
		}
	}
	
}
```

### BFS 시간복잡도
정점의 수가 n이고, 간선의 수가 e인 그래프의 경우

- 그래프가 인접 리스트로 표현된 경우 O(n+e)
- 인접 행렬로 표현된 경우 O(n^2)이다.
희소 그래프인 경우 인접 리스트의 사용이 인접 행렬보다 유리

(희소 그래프는 그래프 내에 적은 수의 간선을 가지는 그래프로 인접 행렬을 사용하면 메모리의 낭비가 크기 때문)