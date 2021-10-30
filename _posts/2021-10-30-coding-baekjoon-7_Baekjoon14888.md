---
title: 백준 14888(연산자 끼워넣기) - 백트래킹
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/14888>
### N개의 수와 N-1개의 연산자가 주어졌을 때, 만들 수 있는 식의 결과가 최대인 것과 최소인 것을 구하는 프로그램을 작성하시오.
첫째 줄에 수의 개수 N(2 ≤ N ≤ 11)가 주어진다. 둘째 줄에는 A1, A2, ..., AN이 주어진다. (1 ≤ Ai ≤ 100) 셋째 줄에는 합이 N-1인 4개의 정수가 주어지는데, 차례대로 덧셈(+)의 개수, 뺄셈(-)의 개수, 곱셈(×)의 개수, 나눗셈(÷)의 개수이다.   

첫째 줄에 만들 수 있는 식의 결과의 최댓값을, 둘째 줄에는 최솟값을 출력한다. 연산자를 어떻게 끼워넣어도 항상 -10억보다 크거나 같고, 10억보다 작거나 같은 결과가 나오는 입력만 주어진다. 또한, 앞에서부터 계산했을 때, 중간에 계산되는 식의 결과도 항상 -10억보다 크거나 같고, 10억보다 작거나 같다.
<hr>
수와 연산자의 개수가 주어질 때 최대와 최소를 구하는 문제로 +, -, /, * 연산자의 개수를 저장할 int형 배열과 숫자를 저장할 배열이 필요하다.    
<br>

```java
public class Step34_14888 {
    public static int[] operator = new int[4];
    public static int[] arr;
    public static int max = -1000000000;
    public static int min = 1000000000;
    public static int N;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();

        N = Integer.parseInt(br.readLine());
        arr = new int[N];
        
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < 4; i++) {
            operator[i] = Integer.parseInt(st.nextToken());
        }

        dfs(arr[0], 1);

        sb.append(max).append('\n').append(min);
        System.out.println(sb);
    }
}
```

dfs(arr[0], 1)은 현재 숫자와 다음 수의 인덱스를 가지고 가는 거다. 지금까지 계산된 결과와 다음 수의 인덱스를 가지고 가는 걸로 생각하면 된다.    

dfs에서 N개의 수를 다 연산했다면 max와 min을 비교하고 리턴하면 된다.    
그리고 연산자 네 개를 확인해야되므로 for문은 네 번 도는 식으로 만들면 된다.    

```java
public static void dfs(int n, int idx) {
    if (idx == N) {
        max = n > max ? n : max;
        min = n < min ? n : min;
        return;
    }

    for (int i = 0; i < 4; i++) {
        if (operator[i] > 0) {
            operator[i]--;

            dfs(getRet(n, idx, i), idx + 1);

            operator[i]++;
        }
    }
}
```

getRet은 연산을 실행하는 메소드로 i가 연산자를 가리키고 있는 것이다. 계산 결과를 리턴해 다시 재귀를 실행하도록 한다.    

```java
public static int getRet(int n, int idx, int o) {
    if (o == 0) return n + arr[idx];
    else if (o == 1) return n - arr[idx];
    else if (o == 2) return n * arr[idx];
    return n / arr[idx];
}
```

완성된 코드는 아래와 같다.


```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step34_14888 {
    public static int[] operator = new int[4];
    public static int[] arr;
    public static int max = -1000000000;
    public static int min = 1000000000;
    public static int N;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();

        N = Integer.parseInt(br.readLine());
        arr = new int[N];
        
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < 4; i++) {
            operator[i] = Integer.parseInt(st.nextToken());
        }

        dfs(arr[0], 1);

        sb.append(max).append('\n').append(min);
        System.out.println(sb);
    }

    public static void dfs(int n, int idx) {
        if (idx == N) {
            max = n > max ? n : max;
            min = n < min ? n : min;
            return;
        }

        for (int i = 0; i < 4; i++) {
            if (operator[i] > 0) {
                operator[i]--;

                dfs(getRet(n, idx, i), idx + 1);

                operator[i]++;
            }
        }
    }

    public static int getRet(int n, int idx, int o) {
        if (o == 0) return n + arr[idx];
        else if (o == 1) return n - arr[idx];
        else if (o == 2) return n * arr[idx];
        return n / arr[idx];
    }
}
```
