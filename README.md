# AlgorithmStudy with Clean Code

---
## 자료 구조(Data Structure) 부터 알고리즘 정복!!

1. 죽은 Readme 파일이 아닌 살아있는 Readme 파일을 만들자.
2. 클린코드에 대해서 같이 일하기 좋은 코드란 무엇일까?
    
    2-1. 클린코드 애자일 소프트웨어 장인 정신 다 읽기 프로젝트
    2-2. 직접 구현해보면서..!!

---
백준 / 프로그래머스를 통한 문제풀이 프로젝트 🛴

프로그래머스 3단계까지 다풀고
백준도 골드이상까지 풀고
문제 없어서 못 풀 때까지 계속되는 프로젝트!


[Check Up! 🧾]
- [x] 그리디 문제
- [ ] 구현
- [ ] 탐색 / 완전 탐색, BFS, DFS
- [ ] 기본 동적 프로그래밍

그 밖에..
- [ ] 행렬 회전
- [ ] SQL 문제...

---
## 하루에 하나씩 알고리즘 시작!


## 자료구조도 하나씩!!

- [ ] Java Collections Framework
- [x] List Interface
- [x] ArrayList
- [ ] Singly LinkedList
- [ ] Doubly LinkedList
- [ ] Stact Interface
- [ ] Stack
- [ ] Queue Interface
- [ ] 배열을 이용한 Queue
- [ ] 연결리스트를 이용한 Queue
- [ ] 배열을 이용한 Deque
- [ ] 연결리스트를 이용한 Deque
- [ ] 배열을 이용한 Heap
- [ ] Priority Queue
- [ ] Set Interface
- [ ] Hash Set
- [ ] Linked Hash Set
---


---
## 알고리즘 Tip

```java
        //1번
        System.out.printf("%d %d\n",val++,val);
        
        //2번
        System.out.printf("%d %d\n",++val,val);
```
> 1번은 val을 출력하고 +1 진행 / 2번은 +1을 하고 출력
---
```java
char ch = (char)(Math.random() * (end-start+1) + start);
```

> start 부터 end 까지의 랜덤 난수 생성;
---
```java
    public void 자리수다더하기() {
        int num = 12345;

        // 결과 저장
        int sum = 0;

        while (num != 0) {
            sum += num%10;
            num /= 10;
        }
    }

    public void 자리수다곱하기() {
        int num = 12345;

        // 결과 저장
        int sum = 0;

        while (num != 0) {
            sum *= num%10;
            num /= 10;
        }
    }

    public void 일부터N까지더하기() {
        int num = 50;

        int val = (num*(num+1))/2;
    }

    public void 소수의갯수구하기(int end) {
        int count = 0;

        // 해당 위치의 index가 true면 소수가 아니라는 의미로 사용
        boolean check[] = new boolean[end+1];

        for(int i=2; i <= end; i++){
            // check[i]가 true면 소수임
            if(check[i] == false){
                count++;
                // i*i부터 시작해 i를 더해가며 아닌 것들을 모두 제외시킴
                // 숫자가 커서 overflow가 날 수 있어 1보다 크다는 조건 추가
                for(int j= i*i; j > 1 && j <= end; j+=i){
                    check[j] = true;
                }
            }
        }
        System.out.println("소수의 개수 : " + count);
    }
```


## 오류일기

---

- intellij 가 실행속도가 느린 것 같아서 vm option을 변경하여서 에러가 발생

> -server
>
> -Xms2g
>
> -Xmx2g
>
> -XX: NewRatio=3
>
> -Xss16m
>
> -XX: +UseConcMarkSweepGC
>
> -XX: +CMSParallelRemarkEnabled
>
> -XX: ConcGCThreads=4
>
> -XX: ReservedCodeCacheSize=240m
>
> -XX: +AlwaysPreTouch
>
> -XX: +TieredCompilation
>
> -XX: +UseCompressed0ops
>
> -XX: SoftRefLRUPolicyMSPerMB=50
>
> -Dsun.io.useCanonCaches=false
>
> -Djava.net.preferIPv4Stack=true
>
> -Djsse.enableSNIExtension=false
>
> -ea


- 으로 변경하였는데, jvm 이 맞지 않다고 하는 에러가 뜨면서 intellij 가 열리지 않았음.
- 이후 bin 파일을 들어가 idea64.exe.vmoptions 을 기존대로 수정하였지만
- 계속 반영되지 않았음.
- 결국 새로 깔았다...
+ 찾아보니.. 사람들도 vmoptions 파일을 수정했지만 여전히 계속되는 error를 겪고있었고, 파일을 삭제하니 해결됬다고 한다..