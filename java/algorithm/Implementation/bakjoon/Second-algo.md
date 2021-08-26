# 구현(Implementation)

---
- 구현이란, 머릿속에 있는 알고리즘을 소스코드로 바꾸는 과정이다.


---
## <문제> 상하좌우

- 여행가 A는 N x N 크기의 정사각형 공간 위에 서 있다. 이 공간은 1 X 1 크기의 정사각형으로 나누어져 있다.

    - 가장 왼쪽 위 좌표는 (1,1) 이며, 가장 오른쪽 아래 좌표는 (N, N)에 해당된다.
    - 여행가 A는 **상, 하, 좌, 우 방향으로 이동**할 수 있으며, 시작 좌표는 항상 (1,1)이다.
    - 우리 앞에는 여행가 A가 이동할 계획이 적힌 계획서가 놓여 있다.<br>

    
- 계획서에는 하나의 줄에 띄어쓰기를 기준으로 하여, L, R, U, D중 하나의 문자가 반복적으로 적혀 있다. 각 문자의 의미는 다음과 같다.<br>

> L : 왼쪽으로 한 칸 이동
> 
> R : 오른쪽으로 한 칸 이동
> 
> U : 위로 한 칸 이동
> 
> D : 아래로 한 칸 이동


- 이 때 여행가 A가 N x N 크기의 정사각형 공간을 벗어나는 움직임은 무시된다. 예를 들어 (1,1) 위치에서 L 혹은 U를 만나면 무시된다.<br>

> - 조건
> > 1. 첫째 줄에 공간의 크기를 나타내는 N이 주어진다. (1 <= N <= 100)
> > 2. 둘째 줄에 여행가 A가 이동할 계획서 내용이 주어진다. (1 <= 이동횟수 <= 100)
> > 3. 첫째 줄에 여행가 A가 최종적으로 도착할 지점의 좌표 (X, Y)를 공백을 기준으로 구분하여 출력하여라.

---

# 내 소스 코드

---
```java
    private String fourthTest(int a, String txt) {
        String result = "";
        String[] plans = txt.split(" ");

        int x = 1, y = 1;

        int[] dx = {0,0,-1,1};
        int[] dy = {-1,1,0,0};
        char[] moveTypes = {'L','R','U','D'};

        for (int i = 0; i<plans.length; i++) {
            char plan = plans[i].charAt(0);

            int nx = 0, ny = 0;
            for (int j = 0; j < 4; j++) {
                if (plan == moveTypes[j]) {
                    nx = x + dx[j];
                    ny = y + dy[j];
                }
            }
            if (nx <1 || ny < 1 || nx > a || ny > a) continue;

            x = nx;
            y = ny;
        }
        result = x + " " + y;
        return result;
    }

```
