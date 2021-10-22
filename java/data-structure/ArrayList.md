ArrayList는 다른 자료구조와 달리 Object[] 배열(객체 배열)을 두고 사용한다는 점이다. 일단은 다른 자료구조는 살펴보지 않았으니 이렇다는 정도만 알고계시면 될 것 같다.



또한 모든 자료구조는 '동적 할당'을 전제로 한다. 가끔 ArrayList를 구현 할 때, 리스트가 꽉 차면 리스트의 크기를 늘리지 않고 그냥 꽉 찼다고 더이상 원소를 안받도록 구현한 경우가 많은데 이는 자료구조를 구현하는 의미가 없다.



동적 할당을 안하고 사이즈를 정해놓고 구현한다면 메인함수에서 정적배열을 선언하는 것과 차이가 없다.



데이터의 개수를 알 수 없는데 배열을 쓰고 싶을 때 여러분은 어떤 방법을 선택하는가? ArrayList, LinkedList 등의 자료구조를 선택할 것이다. 왜냐면 사이즈를 정하지 않고 동적으로 활용할 수 있기 때문이다.





마지막으로 리스트 계열 자료구조는 데이터 사이에 빈 공간을 허락하지 않는다.

아래 예를 들어보자.



Object[] a = {"a", "b", "c", "d"};

이러한 배열이 있고, 만약 "c"라는 데이터를 삭제하려고 한다. (a[2] = null)



그러면 a배열은 다음과 같은 상황일 것이다.

Object[] a = {"a", "b", null, "d"};



이렇게 데이터 사이에 빈 공간이 생길 경우 빈공간을 없애야 한다. 즉, null 뒤에 있는 모든 데이터를 한 칸씩 끌어와야한다는 것이다. 아래와 같이 말이다.

Object[] a = {"a", "b", "d", null};



이렇게 항상 리스트 계열 자료구조는 데이터들이 '연속되어'있어야 한다는 점을 기억하자.