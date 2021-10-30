---
title: 백준 15651(N과 M(3)) - 백트래킹
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/15651>
### 자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오. (1부터 N까지 자연수 중에서 M개를 고른 수열, 같은 수를 여러 번 골라도 된다.)

첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)     

한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다. 중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.    
수열은 사전 순으로 증가하는 순서로 출력해야 한다.    
<hr>
 
이번에는 중복을 허용한다. 중복을 허용한다는 거는 1무터 4까지 두 개의 수를 뽑을 때,    
1 1<br>
1 2<br>
1 3<br>
1 4<br>
2 1<br>
2 2<br>
...<br>
4 4<br>
이렇게 같은 수가 나와도 된다는 것으로, 즉 처음부터 끝까지 다 보라는 거다.    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class prac {
    public static StringBuilder sb = new StringBuilder();
    public static int N, M;
    public static int[] arr;

    public static void Step32_15651(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        
        arr = new int[M];

        dfs(0);        
        System.out.println(sb);
    }

    public static void dfs(int depth) {
        if (depth == M) {
            for (int a : arr) {
                sb.append(a).append(' ');
            }
            sb.append('\n');
            return;
        }

        for (int i = 0; i < N; i++) {
            arr[depth] = i + 1;
            dfs(depth + 1);
        }
    }
}
```

처음부터 끝까지 살피면 되므로 for문에서 항상 처음부터 보면 된다.    
![image](https://user-images.githubusercontent.com/68698007/139520705-b21b80d2-d6f0-42b7-abd1-3cf52a35f6ab.png)
