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

```java
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        for (int tc = 1; tc <= T; tc++) {
            int k = Integer.parseInt(br.readLine());
            Map<Integer, Integer> map = new HashMap<>();
            PriorityQueue<Integer> minQue = new PriorityQueue<>();
            PriorityQueue<Integer> maxQue = new PriorityQueue<>(Collections.reverseOrder());

            for (int i = 0; i < k; i++) {
                String[] input = br.readLine().split(" ");
                char ch = input[0].charAt(0);
                int n = Integer.parseInt(input[1]);

                if (ch == 'I') {
                    map.put(n, map.getOrDefault(n, 0) + 1);

                    minQue.add(n);
                    maxQue.add(n);
                } else {
                    if (map.size() == 0)
                        continue;

                    PriorityQueue<Integer> que = n == 1 ? maxQue : minQue;
                    removeMap(que, map);
                }
            }

            if (map.size() == 0)
                System.out.println("EMPTY");
            else {
                int n = removeMap(maxQue, map);
                System.out.println(n + " " + (map.size() > 0 ? removeMap(minQue, map) : n));
            }

        }

    }

    static int removeMap(PriorityQueue<Integer> que, Map<Integer, Integer> map) {
        int num;
        while (true) {
            num = que.poll();
            int cnt = map.getOrDefault(num, 0);

            if (cnt == 0)
                continue;

            if (cnt == 1)
                map.remove(num);
            else
                map.put(num, cnt - 1);

            break;
        }

        return num;
    }

}
```