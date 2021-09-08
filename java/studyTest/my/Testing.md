# 12865번 평범한 배낭

---
## 문제 

이 문제는 아주 평범한 배낭에 관한 문제이다.

한 달 후면 국가의 부름을 받게 되는 준서는 여행을 가려고 한다. 세상과의 단절을 슬퍼하며 최대한 즐기기 위한 여행이기 때문에, 가지고 다닐 배낭 또한 최대한 가치 있게 싸려고 한다.

준서가 여행에 필요하다고 생각하는 N개의 물건이 있다. 각 물건은 무게 W와 가치 V를 가지는데, 해당 물건을 배낭에 넣어서 가면 준서가 V만큼 즐길 수 있다. 아직 행군을 해본 적이 없는 준서는 최대 K만큼의 무게만을 넣을 수 있는 배낭만 들고 다닐 수 있다. 준서가 최대한 즐거운 여행을 하기 위해 배낭에 넣을 수 있는 물건들의 가치의 최댓값을 알려주자.

## 입력

첫 줄에 물품의 수 N(1 ≤ N ≤ 100)과 준서가 버틸 수 있는 무게 K(1 ≤ K ≤ 100,000)가 주어진다. 두 번째 줄부터 N개의 줄에 거쳐 각 물건의 무게 W(1 ≤ W ≤ 100,000)와 해당 물건의 가치 V(0 ≤ V ≤ 1,000)가 주어진다.

입력으로 주어지는 모든 수는 정수이다.

## 출력

한 줄에 배낭에 넣을 수 있는 물건들의 가치합의 최댓값을 출력한다.

### 예제 입력1

> 4 7
>
> 6 13
>
> 4 8
>
> 3 6
>
> 5 12


### 예제 출력1
> 14


---
이 문제는 배낭 문제(knapsack)로 매우 유명한 문제다. 문제 설명처럼 배낭에 넣을 수 있는 최댓값이 정해지고 해당 한도 물건을 넣어 가치의 합이 최대가 되도록 고르는 방법을 찾는 것이다. 즉, 조합 최적화 문제다.

배낭문제, 일명 냅색 알고리즘은 크게 두 가지 문제로 분류 될 수 있는데, 짐을 쪼갤 수 있는 경우와 짐을 쪼갤 수 없는 경우로 나눌 수 있다. 짐을 쪼갤 수 있는 배낭문제를 Fraction Knapsack Problem 이라 하고, 짐을 쪼갤 수 없는 배낭문제를 0/1 Knapsack Problem 이라 한다. 알고리즘 또한 다르게 적용하는데, Fraction Knapsack Problem 의 경우 탐욕 알고리즘(Greedy)을 쓰며, 0/1 Knapsack Problem의 경우 DP 법을 쓴다. (물론 FPTAS(Fully polynomial time approximation scheme) 으로 스케일링을 통한 방법도 있지만 근사치를 얻는 방법인지라 자칫 틀릴 수도 있다.)

이번 문제는 짐을 쪼갤 수 없기 때문에 다이나믹 프로그래밍(DP)로 해결해야한다.

- dp(i, k) = f(i-1, k), max(f(i-1, k-w)+v, f(i-1,k))로 판별식 세우기

```java
    public static void main(String[] args) throws Exception{
        //bottom-up
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine(), " ");

        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());

        w = new int[n+1];
        v = new int[n+1];
        dp = new int[n+1][k+1];

        for (int i = 1; i <= n; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            w[i] = Integer.parseInt(st.nextToken());
            v[i] = Integer.parseInt(st.nextToken());
        }
        
        for (int i =1; i<=n; i++) {
            for (int j=1; j<=k; j++) {
                if (w[i] > j) {
                    dp[i][j]= dp[i-1][j];
                } else {
                    dp[i][j]= Math.max(dp[i-1][j],dp[i-1][j-w[i]]+v[i]);
                }
            }
        }
    }
```


# 1655번 평범한 배낭

---

## 문제

백준이는 동생에게 "가운데를 말해요" 게임을 가르쳐주고 있다. 백준이가 정수를 하나씩 외칠때마다 동생은 지금까지 백준이가 말한 수 중에서 중간값을 말해야 한다. 만약, 그동안 백준이가 외친 수의 개수가 짝수개라면 중간에 있는 두 수 중에서 작은 수를 말해야 한다.

예를 들어 백준이가 동생에게 1, 5, 2, 10, -99, 7, 5를 순서대로 외쳤다고 하면, 동생은 1, 1, 2, 2, 2, 2, 5를 차례대로 말해야 한다. 백준이가 외치는 수가 주어졌을 때, 동생이 말해야 하는 수를 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에는 백준이가 외치는 정수의 개수 N이 주어진다. N은 1보다 크거나 같고, 100,000보다 작거나 같은 자연수이다. 그 다음 N줄에 걸쳐서 백준이가 외치는 정수가 차례대로 주어진다. 정수는 -10,000보다 크거나 같고, 10,000보다 작거나 같다.

## 출력

한 줄에 하나씩 N줄에 걸쳐 백준이의 동생이 말해야 하는 수를 순서대로 출력한다.


### 들어오는 순서에 따라 정렬 후 최소값. 힙을 사용???


```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Backjoon1655 {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

    public static void main(String[] args) throws IOException {
        int n = Integer.parseInt(br.readLine());
        StringBuilder sb = new StringBuilder();

        PriorityQueue<Integer> minHeap = new PriorityQueue<>((o1, o2) -> o1 - o2);
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>((o1, o2) -> o2 - o1);

        for(int i = 0 ; i < n; i++){
            int num = Integer.parseInt(br.readLine());

            if(minHeap.size() == maxHeap.size()) maxHeap.offer(num);
            else minHeap.offer(num);

            if(!minHeap.isEmpty() && !maxHeap.isEmpty())
                if(minHeap.peek() < maxHeap.peek()){
                    int tmp = minHeap.poll();
                    minHeap.offer(maxHeap.poll());
                    maxHeap.offer(tmp);
                }

            sb.append(maxHeap.peek() + "\n");
        }
        System.out.println(sb);
    }
}
```

# 3197번 백조의 호수

## 문제

두 마리의 백조가 호수에서 살고 있었다. 그렇지만 두 마리는 호수를 덮고 있는 빙판으로 만나지 못한다.

호수는 행이 R개, 열이 C개인 직사각형 모양이다. 어떤 칸은 얼음으로 덮여있다.

호수는 차례로 녹는데, 매일 물 공간과 접촉한 모든 빙판 공간은 녹는다. 두 개의 공간이 접촉하려면 가로나 세로로 닿아 있는 것만 (대각선은 고려하지 않는다) 생각한다.

아래에는 세 가지 예가 있다.

> ...XXXXXX..XX.XXX<br>
....XXXXXXXXX.XXX <br>
...XXXXXXXXXXXX.. <br>
..XXXXX..XXXXXX.. <br>
.XXXXXX..XXXXXX.. <br>
XXXXXXX...XXXX... <br>
..XXXXX...XXX.... <br>
....XXXXX.XXX.... <br>
처음       <br>


>  ....XXXX.......XX <br>
 .....XXXX..X..... <br>
 ....XXX..XXXX.... <br>
 ...XXX....XXXX... <br>
 ..XXXX....XXXX... <br>
 ..XXXX.....XX.... <br>
 ....XX.....X..... <br>
 .....XX....X..... <br>
첫째 날             <br>

> .....XX.......... <br>
 ......X.......... <br>
 .....X.....X..... <br>
 ....X......XX.... <br>
 ...XX......XX.... <br>
 ....X............ <br>
 ................. <br>
 ................. <br>
둘째 날 <br>


백조는 오직 물 공간에서 세로나 가로로만(대각선은 제외한다) 움직일 수 있다.

며칠이 지나야 백조들이 만날 수 있는 지 계산하는 프로그램을 작성하시오.

## 입력

입력의 첫째 줄에는 R과 C가 주어진다. 단, 1 ≤ R, C ≤ 1500.

다음 R개의 줄에는 각각 길이 C의 문자열이 하나씩 주어진다. '.'은 물 공간, 'X'는 빙판 공간, 'L'은 백조가 있는 공간으로 나타낸다.

## 출력

첫째 줄에 문제에서 주어진 걸리는 날을 출력한다.

## 예제 입력 1

> 10 2 <br>
.L <br>
.. <br>
XX <br>
XX <br>
XX <br>
XX <br>
XX <br>
XX <br>
.. <br>
.L <br>


## 예제 출력 1
> 3


## 예제 입력 2
> 4 11 <br>
..XXX...X.. <br>
.X.XXX...L. <br>
....XXX..X. <br>
X.L..XXX... <br>


## 예제 출력 2
> 2

## 예제 입력 3
> 8 17 <br>
...XXXXXX..XX.XXX <br>
....XXXXXXXXX.XXX <br>
...XXXXXXXXXXXX.. <br>
..XXXXX.LXXXXXX.. <br>
.XXXXXX..XXXXXX.. <br>
XXXXXXX...XXXX... <br>
..XXXXX...XXX.... <br>
....XXXXX.XXXL... <br>

## 예제 출력 3
> 2