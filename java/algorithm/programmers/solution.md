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


## kakao internship

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fboyfj2%2FbtrlY4HKvzv%2F8NThzAnXW8cEx0r6rhTAQk%2Fimg.png)

> 문자열 문제로 


```java

    public int solution(String s) {
        String answer = "";
        String sb = "";

        Map<String, Integer> alphabet = new HashMap<>() {{
            put("zero", 0);
            put("one", 1);
            put("two", 2);
            put("three", 3);
            put("four", 4);
            put("five", 5);
            put("six", 6);
            put("seven", 7);
            put("eight", 8);
            put("nine", 9);
        }};



        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);

            if (97 <= ch && ch <= 122) {
                sb += String.valueOf(ch);
            } else if (48 <= ch && ch <= 57) {
                answer += String.valueOf(ch);
            }

            if(alphabet.get(sb) != null) {
                answer += alphabet.get(sb);
                sb = "";
            }
        }

        return Integer.parseInt(answer);
    }

```

> 이렇게 풀었다가
> replaceAll 이 뒤늦게 생각났다....


```java
    public int solution(String s) {
        String[] strArr = {"zero","one","two","three","four","five","six","seven","eight","nine"};

        for (int i = 0; i<10; i++) {
            s = s.replaceAll(strArr[i],Integer.toString(i));
        }

        return Integer.parseInt(s);
    }
```