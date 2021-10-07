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

ArrayList는 Object[] 배열을 사용하면서 내부 구현을 통해 동적으로 관리를 한다. 우리가 흔히 쓰는 primitive 배열(ex int[])과 유사한 형태라고 보면 된다. 즉, 최상위 타입인 Object 타입으로 배열을 생성하여 사용하기 때문에 요소 접근(access elements)에서는 탁월한 성능을 보이나, 중간의 요소가 삽입, 삭제가 일어나는 경우 그 뒤의 요소들은 한 칸씩 밀어야 하거나 당겨야 하기 때문에 삽입, 삭제에서는 비효율적인 모습을 보인다. 