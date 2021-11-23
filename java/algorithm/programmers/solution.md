## 2021 kakao blind recuritment

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcgVXAM%2FbtrlZvY7mmw%2FKmBXhSTuQe8IsavSJmzNkK%2Fimg.png)

> 1단계에 속하는 문자열 문제


```java
    private static String solution(String new_id) {
        //1단계
        String answer = new_id.toLowerCase();

        //2단계
        answer = answer.replaceAll("[^a-z0-9-_.]","");

        //3단계
        while(answer.contains("..")) {
            answer = answer.replace("..",".");
        }

        //4단계
        if (answer.length() > 0) {
            if(String.valueOf(answer.charAt(0)).equals(".")) {
                answer = answer.substring(1,answer.length());
            }
        }

        if (answer.length() > 0) {
            if(String.valueOf(answer.charAt(answer.length()-1)).equals(".")) {
                answer = answer.substring(0,answer.length()-1);
            }
        }

        //5단계
        if (answer.length() == 0) {
            answer += "a";
        }

        //6단계
        if (answer.length() >= 16) {
            answer = answer.substring(0,15);

            if(String.valueOf(answer.charAt(answer.length()-1)).equals(".")) {
                answer = answer.substring(0,answer.length()-1);
            }
        }

        //7단계
        if (answer.length() <= 2) {
            char ch = answer.charAt(answer.length() - 1);
            for (int i =answer.length(); i < 3; i++) {
                answer += String.valueOf(ch);
            }
        }

        return answer;
    }
```
