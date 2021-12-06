---
title: 백준 1149(RGB거리) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/9461>
### 각각의 집을 빨강, 초록, 파랑으로 칠하는 비용이 주어졌을 때, 아래 규칙을 만족하면서 모든 집을 칠하는 비용의 최솟값을 구해보자.
- 1번 집의 색은 2번 집의 색과 같지 않아야 한다.
- N번 집의 색은 N-1번 집의 색과 같지 않아야 한다.
- i(2 ≤ i ≤ N-1)번 집의 색은 i-1번, i+1번 집의 색과 같지 않아야 한다.

첫째 줄에 집의 수 N(2 ≤ N ≤ 1,000)이 주어진다. 둘째 줄부터 N개의 줄에는 각 집을 빨강, 초록, 파랑으로 칠하는 비용이 1번 집부터 한 줄에 하나씩 주어진다. 집을 칠하는 비용은 1,000보다 작거나 같은 자연수이다.    
<hr>
집을 칠하는 비용 중 최솟값을 구하는 것으로 현재 내 집의 색은 이전, 이후의 집 색과 같지 않아야 한다.    

현재 내 집에 들어갈 수 있는 색의 비용이 총 세 개 주어지는 것이므로 [N][3]의 배열이 필요하다. 그 값에는 현재 집에 빨간색을 칠할 경우의 비용, 초록 비용, 파란 색 비용이 들어가고, dp배열에서는 현재 집에 빨간색을 칠할 경우, 이전까지의 값 + 빨간색 비용이 들어가는 것이다.    

dp[0]의 초기값들은 첫번째 집의 각 비용이 될 것이므로 설정해주고 우리는 마지막 집에서 어떤 색을 선택할지에 따라 전체 비용이 달라지니까 N - 1번째 집이 선택하는 색들의 전체 비용 중에 최솟값을 출력하면 된다. 

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step16_1149_1 {
    public static int[][] dp;
    public static int[][] arr;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        dp = new int[N][3];
        arr = new int[N][3];

        StringTokenizer st;
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 3; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        dp[0][0] = arr[0][0];
        dp[0][1] = arr[0][1];
        dp[0][2] = arr[0][2];

        System.out.println(Math.min(RGB(N - 1, 0), Math.min(RGB(N - 1, 1), RGB(N - 1, 2))));
    }
}
```
<br>

그러면 이제 각 비용을 구하는 재귀 함수를 만들어야 한다.    

main에서 Math.min(RGB(N - 1, 0), Math.min(RGB(N - 1, 1), RGB(N - 1, 2)))이렇게 하고 최솟값을 구한 것처럼 재귀에서도 이런 방법을 사용해야 한다.    

- 현재 0(빨강)일 경우: 1(초록) 또는 2(파랑)
- 현재 1(초록)일 경우: 0(빨강) 또는 2(파랑)
- 현재 2(파랑)일 경우: 0(빨강) 또는 1(초록)
현재 집의 색에 따라 이전 집에는 이런 색들이 칠해질 수 있다.    

만약 0을 칠하고자 할 때는 이전 집에 1과 2를 칠했을 때의 전체 비용을 가져온 다음 그 중 최솟값을 선택하고 현재 0을 칠하는데 드는 비용을 더해주면 된다.    

이렇게 하면 첫번째 집에 빨강을 칠할경우부터 시작해 마지막 집에 파랑을 칠할 경우까지의 비용을 구할 수 있다.    


```java
public static int RGB(int n, int c) {
    if (dp[n][c] == 0) {
        if (c == 0) {
            dp[n][0] = Math.min(RGB(n - 1, 1), RGB(n - 1, 2)) + arr[n][0];
        }
        else if (c == 1) {
            dp[n][1] = Math.min(RGB(n - 1, 0), RGB(n - 1, 2)) + arr[n][1];
        }
        else {
            dp[n][2] = Math.min(RGB(n - 1, 0), RGB(n - 1, 1)) + arr[n][2];
        }
    }
    return dp[n][c];
}
```
<br>

#### 전체 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step16_1149_1 {
    public static int[][] dp;
    public static int[][] arr;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        dp = new int[N][3];
        arr = new int[N][3];

        StringTokenizer st;
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 3; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        dp[0][0] = arr[0][0];
        dp[0][1] = arr[0][1];
        dp[0][2] = arr[0][2];

        System.out.println(Math.min(RGB(N - 1, 0), Math.min(RGB(N - 1, 1), RGB(N - 1, 2))));
    }

    public static int RGB(int n, int c) {
        if (dp[n][c] == 0) {
            if (c == 0) {
                dp[n][0] = Math.min(RGB(n - 1, 1), RGB(n - 1, 2)) + arr[n][0];
            }
            else if (c == 1) {
                dp[n][1] = Math.min(RGB(n - 1, 0), RGB(n - 1, 2)) + arr[n][1];
            }
            else {
                dp[n][2] = Math.min(RGB(n - 1, 0), RGB(n - 1, 1)) + arr[n][2];
            }
        }
        return dp[n][c];
    }
}
```
