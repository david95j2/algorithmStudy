# <문제> 1이 될 때까지 
---

- 어떠한 수 N이 1이 될 때까지 다음의 두 과정 중 하나를 반복적으로 선택하여 수행하려고 한다. 단 두 번째 연산은 N이 K로 나누어 떨어질 때만 선택할 수 있다.

>  1. N에서 1을 뺀다.
>  2. N을 K로 나눈다.

>> 예를 들어 N이 17, K가 4일때, 
>>> - 17 - 1 = 16

>>> - 16 / 4 = 4

>>> - 4 / 4 = 1 

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
