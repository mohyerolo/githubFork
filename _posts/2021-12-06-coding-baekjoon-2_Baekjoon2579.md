---
title: 백준 2579(계단 오르기) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/2579>
### 각 계단에 쓰여 있는 점수가 주어질 때 이 게임에서 얻을 수 있는 총 점수의 최댓값을 구하는 프로그램을 작성하시오.
입력의 첫째 줄에 계단의 개수가 주어진다.    

둘째 줄부터 한 줄에 하나씩 제일 아래에 놓인 계단부터 순서대로 각 계단에 쓰여 있는 점수가 주어진다. 계단의 개수는 300이하의 자연수이고, 계단에 쓰여 있는 점수는 10,000이하의 자연수이다.     
<hr>

- 계단은 한 번에 한 계단씩 또는 두 계단씩 오를 수 있다. 즉, 한 계단을 밟으면서 이어서 다음 계단이나, 다음 다음 계단으로 오를 수 있다.
- 연속된 세 개의 계단을 모두 밟아서는 안 된다. 단, 시작점은 계단에 포함되지 않는다.
- 마지막 도착 계단은 반드시 밟아야 한다.

세 개의 규칙을 지키며 최댓값을 구해야한다.    

이전 문제에서 제일 위에서부터 시작해 아래로 내려가면서 최댓값을 구했던 것처럼 이번에도 그렇게 할 것이다.    

```java  
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step16_2579 {
    public static int[] dp;
    public static int[] arr;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        
        arr = new int[N];
        dp = new int[N];

        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(br.readLine());
            dp[i] = -1;
        }

        dp[0] = arr[0];
        // 계단이 하나만 있을 수도 있으므로 dp[1]의 갑은 if문으로 체크해줘야됨
        if (N > 1) {
            dp[1] = arr[0] + arr[1];
        }
        System.out.println(step(N - 1));
    }
}
```

계단을 밟는 과정에서 세 개를 연속해서 밟으면 안 된다. 한 칸, 두 칸 이전의 것을 밟을 수는 있는데 그 값들을 구하는 과정에서 마지막 계단을 밟는 것과 시작점 이전의 것들을 밟는 걸 체크하게 될 수도 있으므로 현재 N의 값이 0 밑으로 내려간다면 0을 반환하도록 해줘야 한다.    

또한 한 칸 이전의 것을 밟았다면 거기서는 또 한 칸 이전의 것을 밟게되면 현재 인덱스에서는 연속으로 세 칸을 밟게 되는 것이다. 그러므로 __현재 인덱스 - 2번째 것을 밟은 것__ 과 __현재 인덱스 - 3번째 것을 밟고 이전 인덱스의 값을 더한 것__ 중에 최댓값을 구한 뒤 현재 값을 더해줘야한다.


```java
public static int step(int n) {
    if (n < 0) return 0;
    if (dp[n] == -1) {
        dp[n] = Math.max(step(n - 2), step(n - 3) + arr[n - 1]) + arr[n];
    }
    return dp[n];
}
```

<br>

#### 전체 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step16_2579 {
    public static int[] dp;
    public static int[] arr;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        
        arr = new int[N];
        dp = new int[N];

        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(br.readLine());
            dp[i] = -1;
        }

        dp[0] = arr[0];
        if (N > 1) {
            dp[1] = arr[0] + arr[1];
        }
        System.out.println(step(N - 1));
    }

    public static int step(int n) {
        if (n < 0) return 0;
        if (dp[n] == -1) {
            dp[n] = Math.max(step(n - 2), step(n - 3) + arr[n - 1]) + arr[n];
        }
        return dp[n];
    }
}
```
