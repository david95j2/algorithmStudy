## 동빈나 알고리즘

---
## 그래프 이론

#### - 간단한 서로소 집합 알고리즘

- 서로 겹치는 소인수가 없는 수.
- 두 자연수가 a, b에 대하여 a와 b의 최대공약수가 1이라면 두 자연수는 서로소이다.

```java
import java.util.*;

public class Main {

    // 노드의 개수(V)와 간선(Union 연산)의 개수(E)
    // 노드의 개수는 최대 100,000개라고 가정
    public static int v, e;
    public static int[] parent = new int[100001]; // 부모 테이블 초기화하기

    // 특정 원소가 속한 집합을 찾기
    public static int findParent(int x) {
        // 루트 노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
        if (x == parent[x]) return x;
        return findParent(parent[x]);
    }

    // 두 원소가 속한 집합을 합치기
    public static void unionParent(int a, int b) {
        a = findParent(a);
        b = findParent(b);
        if (a < b) parent[b] = a;
        else parent[a] = b;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        v = sc.nextInt();
        e = sc.nextInt();

        // 부모 테이블상에서, 부모를 자기 자신으로 초기화
        for (int i = 1; i <= v; i++) {
            parent[i] = i;
        }

        // Union 연산을 각각 수행
        for (int i = 0; i < e; i++) {
            int a = sc.nextInt();
            int b = sc.nextInt();
            unionParent(a, b);
        }

        // 각 원소가 속한 집합 출력하기
        System.out.print("각 원소가 속한 집합: ");
        for (int i = 1; i <= v; i++) {
            System.out.print(findParent(i) + " ");
        }
        System.out.println();

        // 부모 테이블 내용 출력하기
        System.out.print("부모 테이블: ");
        for (int i = 1; i <= v; i++) {
            System.out.print(parent[i] + " ");
        }
        System.out.println();
    }
}
```

## 이진 탐색 알고리즘

- 순차 탐색 : 리스트 안에 있는 특정한 **데이터를 찾기 위해 앞에서부터 데이터를 하나씩 확인**하는 방법
- 이진 탐색 : 정렬되어 있는 리스트에서 **탐색 범위를 절반씩 좁혀가며 데이터를 탐색**하는 방법, 이진 탐색은 시작점, 끝점, 중간점을 이용하여 탐색 범위를 설정한다.

#### 이진 탐색의 시간 복잡도

- 단계마다 탐색 범위를 2로 나누는 것과 동일하므로 연산 횟수는 log２ N에 비례한다.

왼쪽 트리에는 자신보다 작은 크기의 데이터를 가지는 노드들만,
오른쪽 트리에는 자신보다 큰 크기의 데이터를 가지는 노드들만 저장하는 이진트리이다.

따라서 데이터를 찾을 때 데이터가 현재 노드의 데이터보다 작다면 왼쪽으로, 크다면 오른쪽으로 향하면 된다.

완전 이진트리는 아닐 수도 있기 때문에 배열이나 리스트를 활용할 수는 없다.



따라서 노드 정보를 가질 수 있는 node 클래스를 만들어서 사용한다.

이 클래스는 데이터정보,부모노드정보,좌측자식노드정보,우측좌식노드정보를 가져야 한다.

그리고 좀 더 쉬운 관리를 위해

root노드 정보를 가지고 있는 tree클래스도 만들어준다.


```java
class Node {
    int value;
    Node leftChild;
    Node rightChild;

    public Node(int value) {
        this.value = value;
        this.leftChild = null;
        this.rightChild = null;
    }
}
```


### 선형시간 & 로그시간

이진 탐색은 순차 탐색에 비해 엄청나게 빠른 속도로 원하는 데이터를 찾을 수 있다.

한 번에 엄청나게 많은 데이터를 검색 범위에서 줄일 수 있기 때문에

1부터 100사이의 숫자 중 검색한다면 어떤 숫자를 찾던지 최대 7번 만에 정답을 찾을 수 있다.


이진탐색을 사용하면 240,000개의 데이터도 최대 18번 만에 답을 찾을 수 있다.

심지어 40억 개의 데이터를 검색한다고 해도 최대 32번 만에 답을 찾을 수 있다.



n개의 원소를 가진 리스트에서 단순 탐색을 사용하면 최대 n번의 탐색이 필요하다.

이 것을 Big O 표기법으로 O(n)이라고 표기하고 선형 시간이라고 부른다.



이진 탐색을 사용하면 최대 log n번만에 답을 찾을 수 있다.

이 것을 Big O 표기법으로 O(log n)이라고 표기하고 로그 시간이라고 부른다.



이진 탐색은 매우 빠른 속도로 데이터를 찾을 수 있지만

반드시 데이터가 정렬되어있어야만 한다.


```javascript

function binarySearch (target, dataArray) {
let low = 0;
let high = dataArray.length - 1;
let mid = Math.floor((high + low) / 2);
while (target !== dataArray[mid]) {
if (target < dataArray[mid]) {
high = mid - 1;
mid = Math.floor((high + low) / 2);
} else {
low = mid + 1;
mid = Math.floor((high + low) / 2);
}
}
return dataArray[mid];
}


출처: https://im-developer.tistory.com/126 [Code Playground]
```
