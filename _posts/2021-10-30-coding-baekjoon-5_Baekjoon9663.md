---
title: 백준 9663(N-Queen) - 백트래킹
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/9663>
### N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다. N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.
첫째 줄에 N이 주어진다. (1 ≤ N < 15)    
첫째 줄에 퀸 N개를 서로 공격할 수 없게 놓는 경우의 수를 출력한다.    
<hr>
체스 문제로 N을 입력받아 퀸을 둘 수 있는 경우의 수를 출력하는 문제다.    

퀸은 자신이 놓인 방향에서 상하좌우, 대각선으로 움직일 수 있으므로 서로 공격할 수 없게 놓으려면 전에 놓인 퀸들의 상하좌우, 대각선의 위치에 있으면 안 되는 것이다.    

이것도 어떻게 풀지 모르겠어서 <https://st-lab.tistory.com/118> 이거를 보고 풀었다.    

일차원 배열 하나를 사용해서 인덱스와 값으로 col, row를 판별한다는 발상이 너무 신기했다.    
<br>

N x N 체스판에 퀸이 N개 놓여야한다. 그러면 dfs문에서 리턴은 depth == N인 경우라고 생각할 수 있다. 퀸이 N개 놓이면 경우의 수를 하나 더해주고 리턴한다.    

```java
public static void dfs(int depth) {
    // NxN에 N개의 퀸이 놓여야됨. 모든 열에 퀸이 하나씩은 있어야됨.
    if (depth == N) {
        count++;
        return;
    }
}
```

재귀를 위한 for문에서는 항상 0부터 살펴보도록 해야한다. 배열에 row값을 넣어두고 그 값을 넣어도 이전까지 넣은 값들과 퀸을 둘 수 있는 규칙에 어긋나지 않는지를 확인해 본 후 가능하면 다음 위치로 이동할 수 있다.    

```java
public static void dfs(int depth) {
    // NxN에 N개의 퀸이 놓여야됨. 모든 열에 퀸이 하나씩은 있어야됨.
    if (depth == N) {
        count++;
        return;
    }

    for (int i = 0; i < N; i++) {
        arr[depth] = i;
        if (possibility(depth)) {
            dfs(depth + 1);
        }
    }
}
```

possibilty는 가능한지를 살펴볼 함수로 퀸이 그 위치에 놓였을 때 전에 놓여졌을 퀸의 위치들과 겹치지 않는지 살펴보는 것이다. 전에 놓인 퀸들의 상하좌우에 있는지, 대각선상에 위치하는지를 보면 된다.    

```java
public static boolean possibility(int depth) {
    for (int i = 0; i < depth; i++) {
        // 같은 행
        if (arr[i] == arr[depth]) return false;
        // 대각선 (열의 차와 행의 차가 같은 경우)
        if (Math.abs(depth - i) == Math.abs(arr[depth] - arr[i])) return false;
    }
    return true;
}
```
대각선상을 구하는걸 짤 수 없었는데 블로그에서 보고 구할 수 있게 됐다.    
<br>

완성된 코드는 아래와 같다.    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step34_9663 {
    public static int N;
    public static int[] arr;
    public static int count;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        N = Integer.parseInt(br.readLine());
        
        arr = new int[N];

        dfs(0);        
        System.out.println(count);
    }

    public static void dfs(int depth) {
        // NxN에 N개의 퀸이 놓여야됨. 모든 열에 퀸이 하나씩은 있어야됨.
        if (depth == N) {
            count++;
            return;
        }

        for (int i = 0; i < N; i++) {
            arr[depth] = i;
            if (possibility(depth)) {
                dfs(depth + 1);
            }
        }
    }

    public static boolean possibility(int depth) {
        for (int i = 0; i < depth; i++) {
            // 같은 행
            if (arr[i] == arr[depth]) return false;
            // 대각선 (열의 차와 행의 차가 같은 경우)
            if (Math.abs(depth - i) == Math.abs(arr[depth] - arr[i])) return false;
        }
        return true;
    }
}
```    
