## collections-framework

---
         선형 자료구조(Linear Data Structure) : 일렬로 연결된 형태
         List, Queue, Deque

         비선형 자료구조(Nonlinear Data Structure) : 거미줄처럼 연결된 형태
         Graph, Tree

         그 밖에 집합 Set : 데이터가 연결되지 않은 형태 like table

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAGpq3%2FbtqI07wkE1A%2FyX10IjGgt6N3G6rkT1Ievk%2Fimg.png)

---

<List Interface를 구현하는 클래스>

1. ArrayList

2. LinkedList

3. Vector (+ Vector를 상속받은 Stack)


<List Interface에 선언된 대표적인 메소드>

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FefYO5c%2FbtqI07cgkG0%2F9kd7yxy8aMkk2c40FWbPZ1%2Fimg.png)

ArrayList는 Object[] 배열을 사용하면서 내부 구현을 통해 동적으로 관리를 한다. 우리가 흔히 쓰는 primitive 배열(ex int[])과 유사한 형태라고 보면 된다.
즉, 최상위 타입인 Object 타입으로 배열을 생성하여 사용하기 때문에 요소 접근(access elements)에서는 탁월한 성능을 보이나, 중간의 요소가 삽입, 
삭제가 일어나는 경우 그 뒤의 요소들은 한 칸씩 밀어야 하거나 당겨야 하기 때문에 삽입, 삭제에서는 비효율적인 모습을 보인다. 

LinkedList는 데이터(item)와 주소로 이루어진 클래스를 만들어 서로 연결하는 방식이다. 데이터와 주소로 이루어진 클래스를 Node(노드)라고 하는데,
각 노드는 이전의 노드와 다음 노드를 연결하는 방식인 것이다.(이중 연결 리스트라고도 한다.) 즉, 객체끼리 연결한 방식이다. 이렇다보니 요소를 검색해야 할 경우
처음 노드부터 찾으려는 노드가 나올 때 까지 연결된 노드들을 모두 방문해야한다는 점에서 성능이 떨어지나, 해당 노드를 삭제, 삽입해야 할 경우 
해당 노드의 링크를 끊거나 연결만 해주면 되기 때문에 삽입, 삭제에서는 매우 좋은 효율을 보인다.

Vector는 자바를 배울 때 그리 자주 보이지는 않는 클래스인데, 기본적으로 ArrayList와 거의 같다고 보면 된다. Object[] 배열을 사용하며 요소 접근에서
빠른 성능을 보인다. 근데 왜 Vector가 있는 것이냐?라고 한다면, 원래 Vector는 Collection Framwork가 도입되기 전부터 지원하던 클래스였다. 
그리고 Vector의 경우 항상 '동기화'를 지원한다. (쉽게 말하면 여러 쓰레드가 동시에 데이터에 접근하려하면 순차적으로 처리하도록 한다.) 
그렇다보니 멀티 쓰레드에서는 안전하지만, 단일 쓰레드에서도 동기화를 하기 때문에 ArrayList에 비해 성능이 약간 느리다.

Stack은 우리가 흔히 생각하는 것처럼 쌓아 올리는 것이다. 전문용어로 말하면 LIFO(Last in First out) 또는 후입선출이라고 하는데, 쉽게 생각하면
우리가 짐을 쌓는다고 생각하면 쉽다. 짐을 쌓아올릴 때 가장 마지막에 쌓은 짐이 가장 위에 있을 것이다. 그리고 짐을 뺄 때도 가장 위에 있는 짐부터 빼게 될 것이다.
가장 대표적인 예시로는 웹페이지 '뒤로가기'가 있다. 우리가 새로운 페이지로 넘어갈 때마다 넘어가기 전 페이지를 스텍에 쌓고, 만약 뒤로가기를 누른다면 
가장 위에 있는 페이지부터 꺼내오는 방식이다.

참고로 Stack의 경우 Vector클래스를 상속받고 있고, java에서 지원하는 Stack 클래스의 메소드들도 뜯어보면 알겠지만, 모두 Vector에 있는 메소드를 이용하여
구현되고 있어 크게 다를 것은 없다. 


---

Queue


Queue Interface(리스트 인터페이스)는 선형 자료구조로 주로 순서가 있는 데이터를 기반으로 '선입선출(先入先出, FIFO : First-in First-out)'을 위해 만들어진 인터페이스다.
흔히 Stack(스택)과 많이 비교를 하는 자료구조다. 큐에 대해 간단하게 말하자면 10, 20, 30, 40 순으로 데이터를 넣고, 데이터를 꺼낼 때(poll) 넣은 순서 그대로 10, 20, 30,
40이 나오는 구조라는 것이다. 이 때 가장 앞쪽에 있는 위치를 head(헤드)라고 부르고, 가장 후위(뒤)에 있는 위치를 tail(꼬리)라고 부른다. 

Collection 구조를 보면 알겠지만, Queue를 상속하고 있는 Deque(덱) 이라는 Interface도 있다. 둘 다 같은 부류인데 Queue는 한쪽 방향으로만(단방향) 삽입 삭제가 가능한 반면,
Deque는 Double ended Queue라는 의미로 양쪽에서 삽입삭제가 가능한 자료구조라 보면 된다. 즉, head에서도 접근 가능하며, tail에서도 접근 가능한 양방향 큐라고 보면 된다.(Queue에서 확장된 형태)

쉽게 예로 들 수 있는 것은 카드 덱(deck)을 생각하면 된다. 카드를 중간에서 뺄 수는 없고, 맨 위에 놓거나, 맨 아래에 놓거나, 맨 위에 것을 빼거나,
맨 아래 것을 뺄 수 있는 것이라 생각하면 된다. (마침 발음도 같아 기억하기 쉬울 것이다.) 

<Queue/Deque Interface를 구현하는 클래스>

1. LinkedList
2. ArrayDeque
3. PriorityQueue


<Queue/Deque Interface에 선언된 대표적인 메소드>

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcfpfoQ%2FbtqI66JL8WF%2FYgwfZ2O1HRhm67NK3CovEk%2Fimg.png)
