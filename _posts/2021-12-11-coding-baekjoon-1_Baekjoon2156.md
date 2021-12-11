---
title: 백준 2156(포도주 시식) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/2156>
### 1부터 n까지의 번호가 붙어 있는 n개의 포도주 잔이 순서대로 테이블 위에 놓여 있고, 각 포도주 잔에 들어있는 포도주의 양이 주어졌을 때, 효주를 도와 가장 많은 양의 포도주를 마실 수 있도록 하는 프로그램을 작성하시오. 
- 포도주 잔을 선택하면 그 잔에 들어있는 포도주는 모두 마셔야 하고, 마신 후에는 원래 위치에 다시 놓아야 한다.
- 연속으로 놓여 있는 3잔을 모두 마실 수는 없다.

예를 들어 6개의 포도주 잔이 있고, 각각의 잔에 순서대로 6, 10, 13, 9, 8, 1 만큼의 포도주가 들어 있을 때, 첫 번째, 두 번째, 네 번째, 다섯 번째 포도주 잔을 선택하면 총 포도주 양이 33으로 최대로 마실 수 있다.     

첫째 줄에 포도주 잔의 개수 n이 주어진다. (1 ≤ n ≤ 10,000) 둘째 줄부터 n+1번째 줄까지 포도주 잔에 들어있는 포도주의 양이 순서대로 주어진다. 포도주의 양은 1,000 이하의 음이 아닌 정수이다.    

첫째 줄에 최대로 마실 수 있는 포도주의 양을 출력한다.    
<hr>
계단 오르기(2579)를 풀어서 좀 더 쉽게 접근할 수 있었다. 그 문제에서는 마지막 계단을 무조건 밟았어야되나 이번 문제에서는 마지막 잔을 무조건 마셔야된다는 조건이 없다.    

마지막 잔을 마시는 경우는 마지막 잔 - 1과 함께 마시거나 마지막 작 - 2번째 잔을 마시고 난 후에 마지막 잔을 마실 수 있는거다. 그러나 이렇게 마시는 경우가, 마지막 잔 - 1번째와 2번째를 함께 마셨을때나 마지막잔 - 1과 -3을 마셨을 때 보다 클지 우리는 알 수 없다.    

즉, __현재 잔을 마시는 경우와 안 마시고 이전 잔을 마신 값중에 큰 값__ 을 알아봐야된다.    

```java
public static int find(int n) {
    if (n < 0) return 0;
    if (dp[n] == -1) {
        dp[n] = Math.max(Math.max(find(n - 2), find(n - 3) + arr[n - 1]) + arr[n], 
        find(n - 1));
    }

    return dp[n];
}
```


#### 전체 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step16_2156 {
    public static int[] arr;
    public static int[] dp;

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

        System.out.println(find(N - 1));
    }

    public static int find(int n) {
        if (n < 0) return 0;
        if (dp[n] == -1) {
            dp[n] = Math.max(Math.max(find(n - 2), find(n - 3) + arr[n - 1]) + arr[n], 
            find(n - 1));
        }

        return dp[n];
    }
}
```
