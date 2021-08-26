# <문제 1> 1이 될 때까지 

---

- 어떠한 수 N이 1이 될 때까지 다음의 두 과정 중 하나를 반복적으로 선택하여 수행하려고 한다. 단 두 번째 연산은 N이 K로 나누어 떨어질 때만 선택할 수 있다.

>  1. N에서 1을 뺀다.
>  2. N을 K로 나눈다.
>
>> 예를 들어 N이 17, K가 4일때, 
>>> - 17 - 1 = 16
>>> - 16 / 4 = 4
>>> - 4 / 4 = 1
>> 
>> 결과적으로 이 경우 전체 과정을 실행한 횟수는 3이 된다.

- N과 K가 주어질 때 1이 될 때까지 1번 혹은 2번의 과정을 수행해야 하는 최소 횟수를 구하는 프로그램을 작성하여라.


---
## 내 소스코드

```java
	private int firstTest(int n, int k) {
		int cnt = 0;
		
		while (true) {
			if (n == 1) break;
			else if (n % k == 0) {
				n = n / k;
				cnt += 1;
				continue;
			} else {
				n -= 1;
				cnt += 1;
			}
		}
		return cnt;
	}
```

- 시간 고려 후 

```java
	private int firstTest(int n, int k) {
		int cnt = 0;
		
		while (true) {
			int target = (n/k)*k;
			cnt += (n - target);
			n = target;
			
			if (n<k) break;
			
			n /= k;
			cnt += 1;
		}
		
		cnt += (n - 1);
		return cnt;
	}
```

---
## 정당성 분석
- 가능하면 최대한 많이 나누는 작업이, 최적의 해를 항상 보장할 수 있을까?<br>
	- N이 아무리 큰 수여도, K로 나눈다면 기하급수적으로 빠르게 줄일 수 있다.<br>
	- 다시 말해 K가 2 이상이기하면, K로 나누는 것이 1을 빼는 것보다 항상 빠르게 N을 줄일 수 있다.<br>
		- 또한 N은 항상 1에 도달하게 된다.(최적의 해가 성립한다)

---
---

# <문제 2> 곱하기 혹은 더하기

---
- 각 자리가 숫자(0 ~ 9)로 이뤄진 문자열 S가 주어졌을 때, 왼쪽부터 오른쪽으로 하나씩 모든 숫자를 확인하며 숫자 사이에 'x' 혹은 '+' 연산자를 넣어
결과적으로 만들어질 수 있는 **가장 큰 수를 구하는 프로그램**을 작성하여라.
  - 단, +보다 x를 먼저 계산하는 일반적인 방식과는 달리, **모든 연산은 왼쪽에서부터 순서대로** 이루어진다고 가정한다.
	
	예를 들어 02984 라는 문자열로 만들 수 있는 가장 큰 수는 
	> ((((0 + 2) x 9) x 8) x 4) = 576 이다.
	> 
	> 또한, 만들어질 수 있는 가장 큰 수는 항상 20억 이하의 정수가 되도력 입력이 주어진다.

---
## 내 소스코드

```java
    private int secondTest(String txt) {
        int result = txt.charAt(0) - '0';
        for (int i = 1; i<txt.length(); i++) {
            int afterNum = txt.charAt(i) - '0';

            if (afterNum <= 1 || result <= 1) {
                result += afterNum;
            } else {
                result *= afterNum;
            }
        }

        return result;
    }
```
---


# <문제 3> 모험가 길드

---
- 한 마을에 모험가가 N명 있다. 모험가 길드에서는 N명의 모험가를 대상을 '공포도'를 측정하였는데, '공포도'가 높은 모험가는 쉽게 공포를 느껴 위험 상황에서
제대로 대처할 능력이 떨어진다.
  
- 모험가 길드장인 동빈이는 모험가 그룹을 안전하게 구성하고자 **공포도가 X인 모험가는 반드시 X명 이상으로 구성한 모험가 그룹에 참여**해야 여행을 떠날 수 
있도록 규정했다.
  
- 동빈이는 최대 몇개의 모험가 그룹을 만들 수 있는지 궁금하다. N명의 모험가에 대한 정보가 주어졌을 때, **여행을 떠날 수 있는 그룹 수의 최댓값**을 구하는 프로그램
을 작성하여라.

---
## 내 소스코드

```java
    private int thirdTest(int a, String txt) {
        int max = 0;
        int cnt = 0;

        int[] b = Arrays.stream(txt.split(" ")).mapToInt(Integer::parseInt).toArray();
        Arrays.sort(b);

        for (int i = 0; i<b.length; i++) {
            cnt += 1;
            if (cnt >= b[i]) {
                max += 1;
                cnt = 0;
            }
        }

        return max;
    }
```