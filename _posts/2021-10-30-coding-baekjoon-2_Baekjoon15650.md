---
title: 백준 15650(N과 M(2)) - 백트래킹
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/15650>
### 자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오. (1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열, 고른 수열은 오름차순이어야 한다.)

첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)     

한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다. 중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.    
수열은 사전 순으로 증가하는 순서로 출력해야 한다.    
<hr>
앞 문제와 같지만 달라진 점은 오름차순으로 되어있는 수열만 출력될 수 있다는 점이다.
15649번에서 풀었던 코드를 조금만 수정하면 된다.    

<br>

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step34_15650 {
    public static StringBuilder sb = new StringBuilder();
    public static int N, M;
    public static int[] arr;

    public static void main(String[] args) throws IOException {
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
            dfs(depth + 1, i + 1);
        }
    }
}
```
중복이 없어야되지만 어차피 오름차순으로 진행하므로 중복이 있을 수가 없다. 그러므로 이번 코드에서는 boolean배열로 체크하는 과정이 없고, 현재 내가 탐색한 수가 무엇인지 알아야 오름차순으로 진행이 가능하므로 매개변수 하나를 더 써준다.    
여기에는 현재 내가 탐색한 수가 들어갈거고 for문을 그 수부터 돌려주면 오름차순으로 저장할 수 있다.    

1을 풀었다면 확실히 좀 더 쉽게 접근할 수 있는 것 같다.    
![image](https://user-images.githubusercontent.com/68698007/139520527-132d88fb-4e67-457e-82f2-bce7bdbad6f0.png)
