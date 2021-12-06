---
title: 백준 1932(정수 삼각형) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/1932>
### 맨 위층부터 시작해서 아래에 있는 수 중 하나를 선택하여 아래층으로 내려올 때, 이제까지 선택된 수의 합이 최대가 되는 경로를 구하는 프로그램을 작성하라. 아래층에 있는 수는 현재 층에서 선택된 수의 대각선 왼쪽 또는 대각선 오른쪽에 있는 것 중에서만 선택할 수 있다.
삼각형의 크기는 1 이상 500 이하이다. 삼각형을 이루고 있는 각 수는 모두 정수이며, 범위는 0 이상 9999 이하이다.    
첫째 줄에 삼각형의 크기 n(1 ≤ n ≤ 500)이 주어지고, 둘째 줄부터 n+1번째 줄까지 정수 삼각형이 주어진다.    
첫째 줄에 합이 최대가 되는 경로에 있는 수의 합을 출력한다.    
<hr>
첫번째 줄에는 항상 하나의 숫자밖에 없을 것이고 마지막 줄에는 N개의 수가 있을 것이다.    

제일 마지막값을 참조하기 위해 dp[N - 1]에는 arr[N - 1]의 값들을 넣어주고 맨 위에서부터 탐색이 가능하도록 해줘야한다.  

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step16_1932 {
    public static int[][] arr;
    public static int[][] dp;
    public static int N;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        arr = new int[N][N];
        dp = new int[N][N];

        StringTokenizer st;
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < i + 1; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
                dp[i][j] = -1;
            }
        }

        for (int i = 0; i < N; i++) {
            dp[N - 1][i] = arr[N - 1][i];
        }

        System.out.println(findMax(0, 0));
    }
}
```

최댓값은 dp[0][0]에 저장된다. 그러므로 우리는 맨 아래(N - 1)에서부터 dp[이전의 값] + arr[현재 값]을 저장하며 더 큰 값을 찾아내야한다. 아래층에 있는 수는 현재 층에서 선택된 수의 대각선 왼쪽 또는 대각선 오른쪽에 있는 것만 가능하다. 이는 현재 인덱스와 같은 것과 현재 인덱스 + 1이 가능하다는거다.     

```java
public static int findMax(int depth, int idx) {
    // N - 1(맨 아래 값)
    if (depth == N -1) return dp[depth][idx];
    if (dp[depth][idx] == -1) {
        dp[depth][idx] = Math.max(findMax(depth + 1, idx), findMax(depth + 1, idx + 1)) + arr[depth][idx];
    }
    return dp[depth][idx];
}
```

#### 전체 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step16_1932 {
    public static int[][] arr;
    public static int[][] dp;
    public static int N;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        arr = new int[N][N];
        dp = new int[N][N];

        StringTokenizer st;
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < i + 1; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
                dp[i][j] = -1;
            }
        }

        for (int i = 0; i < N; i++) {
            dp[N - 1][i] = arr[N - 1][i];
        }

        System.out.println(findMax(0, 0));
    }

    public static int findMax(int depth, int idx) {
        if (depth == N -1) return dp[depth][idx];
        if (dp[depth][idx] == -1) {
            dp[depth][idx] = Math.max(findMax(depth + 1, idx), findMax(depth + 1, idx + 1)) + arr[depth][idx];
        }
        return dp[depth][idx];
    }
}
```
