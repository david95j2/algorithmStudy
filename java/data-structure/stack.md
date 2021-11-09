## stack
---
문제를 풀다보면 스택을 쌓아서 푸는게 훨씬 빠를 때가 있는 것을 깨달았다.
- 역순 문자열 만들기..
- 후위 표기법 검사..!
---
- 같은 구조와 크기의 자료를 정해진 방향으로만 쌓을 수 있다.
- top으로 정한 곳을 통해서만 접근 가능이다.

```java
public static void main(String[] args) {
    Stack<String> stack = new Stack<>();
    
    stack.push("testData");
    
    System.out.println(stack.peek());

    System.out.println(stack.pop());
    
    System.out.println(stack.pop());
        }
```

![image](https://blog.kakaocdn.net/dn/Yz5uV/btqELyK5mOY/xfQD0KlF9DHwBDK2QkhePK/img.png)

