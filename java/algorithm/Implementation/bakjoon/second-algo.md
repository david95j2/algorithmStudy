# 구현(Implementation)

---
- 구현이란, 머릿속에 있는 알고리즘을 소스코드로 바꾸는 과정이다.


---
## <문제 1> 상하좌우

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

<br>

---
## <문제 2> 시각

- 정수 N이 입력되면 00시 00분 00초부터 N시 59분 59초까지의 모든 시각 중에서 3이 하나라도 포함되는 **모든 경우의 수**를 구하는 프로그램을
작성해라. 
  - 예를 들어, 1을 입력했을 때 다음은 3이 하나라도 포함되어 있으므로 세어야 하는 시각이다.
  > 00시 00분 03초
  > 
  > 00시 13분 30초
   
  - 반면에 다음은 3이 하나도 포함되어 있지 않으므로 세면 안 되는 시각이다.
  > 00시 02분 55초
  > 
  > 01시 27분 45초
  
 - 첫째 줄에 정수 N이 입력된다. (0 <= N <= 23)
 - 00시 00분 00초부터 N시 59분 59초까지의 모든 시각 중에서 3이 하나라도 포함되는 모든 경우의 수를 출력한다.

### Tip !
- 이 문제는 가능한 모든 시각의 경우를 하나씩 모두 세서 풀 수 있는 문제이다.
- 하루는 86,400초 이므로, 00시 00분 00초부터 23시 59분 59초까지의 모든 경우의 수는 86,400가지 이다.
  - 24 * 60 * 60 = 86,400
  
- 따라서 단순히 시각을 1씩 증가하면서 3이 하나라도 포함되어 있는지를 확인하면 된다.
- 이러한 유형은 **완전 탐색(Brute Forcing)** 문제 유형이다.
  - 가능한 경우의 수를 모두 검사하는 탐색 방법을 의미한다.
  
## 내 소스코드

---
```java
    public static boolean check(int h, int m, int s) {
        if (h % 10 == 3 || m / 10 == 3 || m % 10 == 3 || s / 10 == 3 || s % 10 ==3) return true;
        return false;
    }

    private int fifthTest(int h) {
        int result = 0;

        for (int i = 0; i<=h; i++) {
            for (int j= 0; j < 60; j++) {
                for (int k = 0; k < 60; k++) {
                    if (check(i,j,k)) result++;
                }
            }
        }
        System.out.println(result);
        return result;
    }
```

---

# <문제 3> 왕실의 나이트

- 행복 왕국의 왕실 정원은 체스판과 같은 8 x 8 좌표 평면이다. 왕실 정원의 특정한 한 칸에 나이트가 서 있다.
나이트는 매우 충성스러운 신하로써 매일 무술을 연마한다.
  
- 나이트는 말을 타고 있기 때문이 이동을 할 때는 L자 형태로만 이동할 수 있으며 정원 밖으로는 나갈 수 없다.

- 나이트는 특정 위치에서 다음과 같은 2가지 경우로 이동이 가능하다.
  > 1. 수평으로 두 칸 이동한 뒤에 수직으로 한 칸 이동하기
  > 2. 수직으로 두 칸 이동한 뒤에 수평으로 한 칸 이동하기

- 이처럼 8 X 8 좌표 평면상에서 나이트의 위치가 주어졌을 때 나이트가 이동할 수 있는 경우의 수를 추력하는 프로그램을 작성하여라.
- 왕실의 정원에서 행 위치를 표현할 때는 1부터 8로 표현하며, 열 위치를 표현할 때는 a부터 h로 표현한다.

  - c2 에 있을 때 이동할 수 있는 경우의 수는 6가지이다.<br>

  > 첫째 줄에 8 x 8 좌표 평면상에서 현재 나이트가 위치한 곳의 좌표를 나타내는 두 문자로 구성된 문자열이 입력된다. 입력 문자는 a1처럼 열과 행으로 이루어진다.
  >  
  > 첫째 줄에 나이트가 이동할 수 있는 경우의 수를 출력하여라.

<br>

---

## 내 소스코드 
```java
    private int sixthTest(String txt) {
        int result = 0;

        int x = txt.charAt(1) - '0';
        int y = txt.charAt(0) - 'a' + 1;

        int[] dx = {-2,-1,1,2,2,1,-1,-2};
        int[] dy = {-1,-2,-2,-1,1,2,2,1};

        for (int i = 0; i< 8; i++) {
            int nx = x + dx[i];
            int ny = y + dy[i];

            if (nx >= 1 && nx <= 8 && ny >= 1 && ny <= 8) {
                result += 1;
            }
        }

        return result;
    }
```

---
## <문제 4> 문자의 재정렬

- 알파벳 대문자와 숫자 (0~9)로만 구성된 문자열이 입력으로 주어진다.
- 이때 모든 알파벳을 오름차순으로 정렬하여 이어서 출력한 뒤에, 그 뒤에 모든 숫자를 더한 값을 이어서 출력해라.

  - 예를 들어, K1KA5CB7 이라는 값이 들어오면 ABCKK13을 출력해라
  
## 내 소스코드

```java
    private void seventhTest(String txt) {
        ArrayList<Character> result = new ArrayList<Character>();
        int num = 0;
        String val = "";

        for (int i = 0; i<txt.length(); i++) {
            if (Character.isLetter(txt.charAt(i))) {
                result.add(txt.charAt(i));
            } else {
                num += txt.charAt(i) - '0';
            }
        }
        Collections.sort(result);

        for (int i =0; i<result.size(); i++) {
            val += result.get(i);
        }
        val += String.valueOf(num);

        System.out.println(val);
    }
```