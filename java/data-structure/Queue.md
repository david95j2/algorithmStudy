## Queue

## Prioirty Queue

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJU1JT%2FbtrlpLQqSHZ%2FotTGNyfzMyqzkQqJZny940%2Fimg.png)

> 최댓값 최솟값만 쏙쏙 뽑아낼 수 있는 자료구조가 보이면 Heap 자료구조가 가장 먼저 떠올릴 수 있다. 트리 형태의 자료구조로 Max Heap은 부모가 자식보다 크거나 같은 값을 갖는 조건을 만족하고 Min Heap은 부모가 자식보다 작거나 같은 값을 갖는다.

1. Heap
   - Max Heap은 부모가 자식보다 크거나 같은 값을 갖는다.

 - push가 되면 가장 끝 노드에 추가가 되고 조건을 만족하도록 정렬이 이루어진다. 새로운 노드를 부모 노드와 비교하면서 부모 노드보다 값이 크면 swap해서 올라간다. 트리 구조이기 때문에 시간 복잡도는 O(logN)이다.

2. priority queue
- priority_queue<type, Container Type, Compare> 로 정의
- 기본적으로 Min Heap이며 Max Heap은 Compare 함수에 greater<Type>을 사용하면 된다.
- Type이 pair인 경우 첫번째 값을 비교해 정렬한다.
- 관련함수는 queue와 유사하다.