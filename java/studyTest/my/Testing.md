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