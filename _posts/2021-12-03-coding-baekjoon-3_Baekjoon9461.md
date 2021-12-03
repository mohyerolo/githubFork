---
title: 백준 9461(파도반 수열) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/9461>
### N이 주어졌을 때, P(N)을 구하는 프로그램을 작성하시오.
나선에서 가장 긴 변의 길이를 k라 했을 때, 그 변에 길이가 k인 정삼각형을 추가한다.

파도반 수열 P(N)은 나선에 있는 정삼각형의 변의 길이이다. P(1)부터 P(10)까지 첫 10개 숫자는 1, 1, 1, 2, 2, 3, 4, 5, 7, 9이다.    

첫째 줄에 테스트 케이스의 개수 T가 주어진다. 각 테스트 케이스는 한 줄로 이루어져 있고, N이 주어진다. (1 ≤ N ≤ 100)    
<hr>
예시로 보여주는 P(1)부터 P(10)까지의 길이로 재귀가 어떻게 돌아갈지를 알 수 있었다.   
P(N) = P(N - 2) + P(N - 3)으로 P(10) = P(8) + P(7) = 5 + 4 = 9가 된다.    

케이스가 최대 100까지 존재할 수 있으므로 배열의 크기는 100로 잡았다.    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    public static int[] dp = new int[100];

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        dp[0] = 1; dp[1] = 1; dp[2] = 1;
        dp[3] = 2; dp[4] = 2;
        dp[5] = 3;
        dp[6] = 4;
        dp[7] = 5;
        dp[8] = 7;
        dp[9] = 9;

        for (int i = 10; i < dp.length; i++) {
            dp[i] = -1;
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < T; i++) {
            sb.append(padovan(Integer.parseInt(br.readLine()) - 1)).append('\n');
        }
        System.out.println(sb);
    }

    public static int padovan(int n) {
        if (dp[n] == -1) {
            dp[n] = padovan(n - 2) + padovan(n - 3);
        }
        return dp[n];
    }
}
```

그런데 제출했더니 틀렸다고 떠서 블로그를 찾아봤더니 int가 아닌 long으로 해야된다는 걸 알게됐다. 예제에서 12는 16이라는 걸 알 수 있어도 long으로 수정하고 100을 해보니 무려 888,855,064,897(8천8백8십8억)이 나온다.    

int의 최댓값은 2,147,483,647로 그 값을 한참 뛰어넘어 int형 배열로는 전체가 돌아갈 수 없게 된다.    
  

#### 최종 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step16_9461 {
    public static long[] dp = new long[100];

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        dp[0] = 1; dp[1] = 1; dp[2] = 1;
        dp[3] = 2; dp[4] = 2;
        dp[5] = 3;
        dp[6] = 4;
        dp[7] = 5;
        dp[8] = 7;
        dp[9] = 9;

        for (int i = 10; i < dp.length; i++) {
            dp[i] = -1;
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < T; i++) {
            sb.append(padovan(Integer.parseInt(br.readLine()) - 1)).append('\n');
        }
        System.out.println(sb);
    }

    public static long padovan(int n) {
        if (dp[n] == -1) {
            dp[n] = padovan(n - 2) + padovan(n - 3);
        }
        return dp[n];
    }
}
```
