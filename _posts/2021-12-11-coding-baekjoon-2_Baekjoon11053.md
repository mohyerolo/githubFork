---
title: 백준 11053(가장 긴 증가하는 부분 수열) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/11053>
### 수열 A가 주어졌을 때, 가장 긴 증가하는 부분 수열을 구하는 프로그램을 작성하시오.
예를 들어, 수열 A = {10, 20, 10, 30, 20, 50} 인 경우에 가장 긴 증가하는 부분 수열은 {10, 20, 30, 50} 이고, 길이는 4이다.    

첫째 줄에 수열 A의 크기 N (1 ≤ N ≤ 1,000)이 주어진다.
둘째 줄에는 수열 A를 이루고 있는 Ai가 주어진다. (1 ≤ Ai ≤ 1,000)    

첫째 줄에 수열 A의 가장 긴 증가하는 부분 수열의 길이를 출력한다.    
<hr>
증가하는 수열의 길이를 출력해야한다.    

배열에 6개의 원소가 들어있다면 dp배열에는 그 원소까지의 증가하는 수열의 길이를 저장하면 된다.    

예시로 나온 {10, 20, 10, 30, 20, 50}의 dp배열에는 {1, 2, 1, 3, 2, 4}가 저장되고 단순히 마지막 배열인 dp[N]을 가져오는 걸로 하며 안 된다. 그렇게 되면 마지막에 온 원소가 만약 50이 아니고 10일 경우에는 1이 출력된다. 그러므로 dp에 저장된 원소 중 가장 큰 값을 가져오면 수열에서 가장 긴 증가하는 길이를 출력할 수 있다.    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step16_11053 {
    public static int[] dp;
    public static int[] arr;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        dp = new int[N];
        arr = new int[N];

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
            dp[i] = -1;
        }

        dp[0] = 1;

        int max = 1;
        // 원소를 훑어가며 max를 찾아야되므로 차례대로 재귀를 통해 알아내도록 한다.
        for (int i = 1; i < N; i++) {
            max = Math.max(max, LIS(i));
        }
        System.out.println(max);
    }
}
```

LIS 메소드에서는 주어진 N번째 원소까지의 증가하는 수열 개수를 알아내면 된다.    
그러므로 for문을 통해 N - 1번째부터 0번째 원소를 훑으며 자기보다 작은 원소의 dp배열에 저장된 개수를 가져오면 된다. 이미 이전의 원소에는 그 원소의 부분 수열 개수가 저장되어있으므로 거기에 1을 더해주면 현재 원소의 부분 수열 개수가 저장되는 것이다.    

```java
public static int LIS(int N) {
    if (dp[N] == -1) {
        dp[N] = 1;
        for (int i = N - 1; i >= 0; i--) {
            if (arr[N] > arr[i]) {
                dp[N] = Math.max(dp[N], LIS(i) + 1);
            }
        }
    }
    return dp[N];
}   
```

#### 전체 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step16_11053 {
    public static int[] dp;
    public static int[] arr;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        dp = new int[N];
        arr = new int[N];

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
            dp[i] = -1;
        }

        dp[0] = 1;

        int max = 1;
        for (int i = 1; i < N; i++) {
            max = Math.max(max, LIS(i));
        }
        System.out.println(max);
    }

    public static int LIS(int N) {
        if (dp[N] == -1) {
            dp[N] = 1;
            for (int i = N - 1; i >= 0; i--) {
                if (arr[N] > arr[i]) {
                    dp[N] = Math.max(dp[N], LIS(i) + 1);
                }
            }
        }
        return dp[N];
    }   
}
```
