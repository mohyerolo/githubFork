---
title: 백준 15652(N과 M(4)) - 백트래킹
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/15652>
### 자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오. (1부터 N까지 자연수 중에서 M개를 고른 수열, 같은 수를 여러 번 골라도 된다, 고른 수열은 비내림차순이어야 한다.)

첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)     

한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다. 중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.    
수열은 사전 순으로 증가하는 순서로 출력해야 한다.    
<hr>
 
비내림차순이라는 거는 만약 1부터 4까지 2개의 수를 골라야할 경우 1은 1부터 4까지, 2는 2부터 4까지, 3은 3과 4, 4는 4만 가능하다는 것이다 (중복 가능할 경우).    

중복이 가능한 오름차순이라는 거다.   

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class prac {
    public static StringBuilder sb = new StringBuilder();
    public static int N, M;
    public static int[] arr;

    public static void Step34_15652(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        
        arr = new int[M];

        dfs(0, 0);        
        System.out.println(sb);
    }

    public static void dfs(int depth, int n) {
        if (depth == M) {
            for (int a : arr) {
                sb.append(a).append(' ');
            }
            sb.append('\n');
            return;
        }

        for (int i = n; i < N; i++) {
            arr[depth] = i + 1;
            dfs(depth + 1, i);
        }
    }
}
```

dfs에서 시작하는 수를 현재 탐색했던 수로 잡고, 반복문의 시작을 그 수로 하면 중복이 가능한 오름차순이 된다.    
![image](https://user-images.githubusercontent.com/68698007/139520842-b18c2fe9-c809-4f19-aead-1b357ea2e327.png)
