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


() 붙어 있으면 레이져,
(...)  막대, 레이져가 막대를 자르는데 잘린 막대의 수

3가지
<br>
( 만난 경우
<br>
) 만난 경우
<br>
레이져를 만난 경우
<br>

```java
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        String ironStick = br.readLine();
        Stack<Character> stack = new Stack<>();
        int part = 0;
        
        for (int i = 0; i < ironStick.length(); i++) {
            if(ironStick.charAt(i)=='('){
                stack.push('(');
            }else {
                if(ironStick.charAt(i-1)=='(') { // 레이져인 경우
                    stack.pop();
                    part+=stack.size();
                }else {
                    ++part;
                    stack.pop();
                }
            }
        }
        System.out.println(part);
    }
}
```

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc2SyeX%2FbtrkJnvWcpx%2FlzDiueCnEMJRFNbHgqrlDk%2Fimg.png)