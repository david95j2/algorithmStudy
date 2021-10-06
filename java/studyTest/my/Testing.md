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


단순 반복 bfs문제 같지만 R,C 범위가 크기 때문에 반복적으로 bfs를 돌리다 보면 메모리 초과나 시간 초과가 발생할 수 있다.

우선 2단계로 풀이가 나누어지는데 1단계는 백조끼리 서로 만날 수 있는지 체크하고 그 다음 물과 인접해있는 얼음을 녹이는 과정이 필요하다.

백조끼리 서로 만나는지 확인하기 위해서는 bfs를 이용하면 되지만 한쪽 백조에서 출발하게 되면 탐색했던 범위를 반복해서 탐색하기 때문에 비효율적이다. 그렇기 때문에 다른쪽 백조를 찾기위해서 bfs탐색 도중 만나게 되는 얼음들을 저장해두었다가 다음 탐색에 사용한다.

다음 단계는 물과 인접해 있는 얼음들을 녹이는 과정인데 여기서도 모든 물의 좌표를 저장해두면 순회하는데 시간이 많이 걸리기 때문에 물과 인접해 있는 얼음(이번에 녹을 얼음)좌표를 저장해두었다가 사용하면 효율적으로 풀이할 수 있다.




## 카카오

```java
static String[] id_list = new String[]{
            "muzi", "frodo", "apeach", "neo"
    };

    public static void main(String[] args) throws IOException {
        String test = "...!@BaT#*..y.abcdefghijklm";
        String[] id_list = new String[]{
                "muzi", "frodo", "apeach", "neo"
        };
        String[] report = new String[]{
                "muzi frodo", "apeach frodo", "frodo neo", "muzi neo", "apeach muzi"
        };
        int k = 2;

        solution(id_list, report, k);
    }

    public static int[] findId(String me, String you) {
        int[] tmp = new int[2];

        for (int i = 0; i < id_list.length; i++) {
            if (id_list[i].equals(me)) {
                tmp[0] += i;
            } else if (id_list[i].equals(you)) {
                tmp[1] += i;
            }
        }
        return tmp;
    }

    public static int[] solution(String[] id_list, String[] report, int k) {
        int[] answer = new int[id_list.length];
        String[][] reportNum = new String[id_list.length][2];

        for (int i = 0; i < id_list.length; i++) {
            for (int j = 0; j < 2; j++) {
                reportNum[i][j] = "";
            }
        }


        for (int i = 0; i < report.length; i++) {
            String[] arr = report[i].split(" ");
            int[] tmp = findId(arr[0], arr[1]);
            if (reportNum[tmp[0]][1].contains(String.valueOf(tmp[1]))) {
                continue;
            }
            reportNum[tmp[0]][1] += tmp[1];
            reportNum[tmp[1]][0] += 1;
        }

        for (int i = 0; i < id_list.length; i++) {
            if (reportNum[i][0].length() >= k) {
                for (int j=0; j<id_list.length; j++) {
                    if (reportNum[j][1].contains(String.valueOf(i))) {
                        answer[j]++;
                    }
                }
            }
        }


        return answer;
    }
```


## 신규 아이디 추천

카카오에 입사한 신입 개발자 네오는 "카카오계정개발팀"에 배치되어, 카카오 서비스에 가입하는 유저들의 아이디를 생성하는 업무를 담당하게 되었습니다. "네오"에게 주어진 첫 업무는 새로 가입하는 유저들이 카카오 아이디 규칙에 맞지 않는 아이디를 입력했을 때, 입력된 아이디와 유사하면서 규칙에 맞는 아이디를 추천해주는 프로그램을 개발하는 것입니다.
다음은 카카오 아이디의 규칙입니다.

아이디의 길이는 3자 이상 15자 이하여야 합니다.
아이디는 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.) 문자만 사용할 수 있습니다.
단, 마침표(.)는 처음과 끝에 사용할 수 없으며 또한 연속으로 사용할 수 없습니다.
"네오"는 다음과 같이 7단계의 순차적인 처리 과정을 통해 신규 유저가 입력한 아이디가 카카오 아이디 규칙에 맞는 지 검사하고 규칙에 맞지 않은 경우 규칙에 맞는 새로운 아이디를 추천해 주려고 합니다.
신규 유저가 입력한 아이디가 new_id 라고 한다면,


> 1단계 new_id의 모든 대문자를 대응되는 소문자로 치환합니다.
>
> 2단계 new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자를 제거합니다.
>
> 3단계 new_id에서 마침표(.)가 2번 이상 연속된 부분을 하나의 마침표(.)로 치환합니다.
>
> 4단계 new_id에서 마침표(.)가 처음이나 끝에 위치한다면 제거합니다.
>
> 5단계 new_id가 빈 문자열이라면, new_id에 "a"를 대입합니다.
>
> 6단계 new_id의 길이가 16자 이상이면, new_id의 첫 15개의 문자를 제외한 나머지 문자들을 모두 제거합니다.
     만약 제거 후 마침표(.)가 new_id의 끝에 위치한다면 끝에 위치한 마침표(.) 문자를 제거합니다.
>
> 7단계 new_id의 길이가 2자 이하라면, new_id의 마지막 문자를 new_id의 길이가 3이 될 때까지 반복해서 끝에 붙입니다.


예를 들어, new_id 값이 "...!@BaT#*..y.abcdefghijklm" 라면, 위 7단계를 거치고 나면 new_id는 아래와 같이 변경됩니다.

1단계 대문자 'B'와 'T'가 소문자 'b'와 't'로 바뀌었습니다.
"...!@BaT#*..y.abcdefghijklm" → "...!@bat#*..y.abcdefghijklm"

2단계 '!', '@', '#', '*' 문자가 제거되었습니다.
"...!@bat#*..y.abcdefghijklm" → "...bat..y.abcdefghijklm"

3단계 '...'와 '..' 가 '.'로 바뀌었습니다.
"...bat..y.abcdefghijklm" → ".bat.y.abcdefghijklm"

4단계 아이디의 처음에 위치한 '.'가 제거되었습니다.
".bat.y.abcdefghijklm" → "bat.y.abcdefghijklm"

5단계 아이디가 빈 문자열이 아니므로 변화가 없습니다.
"bat.y.abcdefghijklm" → "bat.y.abcdefghijklm"

6단계 아이디의 길이가 16자 이상이므로, 처음 15자를 제외한 나머지 문자들이 제거되었습니다.
"bat.y.abcdefghijklm" → "bat.y.abcdefghi"

7단계 아이디의 길이가 2자 이하가 아니므로 변화가 없습니다.
"bat.y.abcdefghi" → "bat.y.abcdefghi"

따라서 신규 유저가 입력한 new_id가 "...!@BaT#*..y.abcdefghijklm"일 때, 네오의 프로그램이 추천하는 새로운 아이디는 "bat.y.abcdefghi" 입니다.

## 문제

신규 유저가 입력한 아이디를 나타내는 new_id가 매개변수로 주어질 때, "네오"가 설계한 7단계의 처리 과정을 거친 후의 추천 아이디를 return 하도록 solution 함수를 완성해 주세요.

## 제한사항

new_id는 길이 1 이상 1,000 이하인 문자열입니다.
new_id는 알파벳 대문자, 알파벳 소문자, 숫자, 특수문자로 구성되어 있습니다.
new_id에 나타날 수 있는 특수문자는 -_.~!@#$%^&*()=+[{]}:?,<>/ 로 한정됩니다.


```java
class Solution {
    public String solution(String new_id) {
        String answer = new_id;
        
        answer = answer.toLowerCase();
        
        for (int i =0; i<answer.length(); i++) {
            int tmp = answer.charAt(i)-'0';
            
            if (97 <= tmp && tmp <= 122)
        }
        
        
        return answer;
    }
}
```

