---
title: 백준 15649(N과 M(1)) - 백트래킹
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/15649>
### 자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오. (1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열)

첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)     

한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다. 중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.    
수열은 사전 순으로 증가하는 순서로 출력해야 한다.    
<hr>
백트래킹 문제로 1부터 N까지의 수가 M번 나오는 모든 경우의 수를 출력하면 된다.    
중복 없이 출력해야하므로 M개의 수에서 한 번 나온 수는 다음에 나오면 안 된다.    

이번 백트래킹 문제들은 전부 <https://st-lab.tistory.com/114> 이 블로그의 도움을 받아 풀었다.    
근데 풀면서도 계속 헷갈리고.. 다시 풀어도 헷갈리니 익숙해지려면 시간이 좀 걸릴 것 같다.    

<br>

자연수 N개가 M번 나와야하므로 __M개의 수를 갖고 있을 배열__ 이 하나 필요하고, 중복이 있으면 안 되므로 __현재 사용됐는지, 아닌지를 확인할 수 있는 배열__ 이 하나 더 필요하다. 

```java
public class Step34_15649 {
    public static StringBuilder sb = new StringBuilder();
    public static int N, M;
    public static int[] arr;
    public static boolean[] check;
}
```
static으로 밖에 선언한 이유는 main함수 외에 사용할 함수에서 계속해서 이 두 개의 배열과 자연수 N, M을 사용하기 때문이다.    
또한 다른 함수에서 StringBuilder의 append()를 이용해 출력할 것을 저장하고 main에서 전체를 출력할 것이므로 StringBuilder도 static으로 선언해준다.    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step34_15649 {
    public static StringBuilder sb = new StringBuilder();
    public static int N, M;
    public static boolean[] check;
    public static int[] arr;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        
        check = new boolean[N];
        arr = new int[M];

        dfs(0);        
        System.out.println(sb);
    }
}
```
틀은 이렇고 dfs(0)함수에서 이제 전체를 훑으며 확인하는 과정을 거칠거다.    

dfs는 depth-first search로 깊이 우선 탐색이다. 백트래킹을 푸는 전형적인 방법 중 하나로 루트 노드에서 시작해 전체를 다 훑는 방법이다.   

dfs(0)에서 0은 현재 내가 탐색하고 있는 높이이기도 하지만 여기서는 내가 담은 수의 개수로 본다. M개를 골라야하는 문제이니까 <mark style='background-color: #fff5b1'> depth가 M이 되면 다 고른 걸로 판단한다. </mark>   

따라서 코드는 아래와 같이 될 것 이다.

```java
public static void dfs(int depth) {
        if (depth == M) {
            for (int a : arr) {
                sb.append(a).append(' ');
            }
            sb.append('\n');
            return;
        }
}
```

내가 담은 개수(depth == 깊이)가 M과 같아지면 길이가 M인 배열 arr에 담긴 원소들을 StringBuilder에 저장해주고 리턴한다.    
이러면 길이가 M인 수열 하나를 발견한 것이다.    

그러면 dfs에서 어떻게 순환을 할 지를 만들어야 한다.    

우리는 중복이 없이 수열을 만들어야 되지만 수열이 오름차순으로는 진행되지 않아도 된다. 그렇다면 반복문에서 시작은 항상 0이어도 되고 N까지 반복하면 되는 것이다.    

```java
for (int i = 0; i < N; i++) {}
```    
중복이 없어야 하므로 만든 boolean배열을 이용해서 만약 사용한 적이 있다면 건너뛰고 없을 경우에는 배열을 true로 만든 후에 arr배열에 값을 저장해주고 재귀를 돌려주면 된다.   

```java
for (int i = 0; i < N; i++) {
    if (!check[i]) {
        check[i] = true;
        arr[depth] = i + 1;
        dfs(depth + 1);
        check[i] = false;
    }
}
```
check[i]는 다음에 다시 참조하기 위해 false로 돌려준다.    

이렇게 모든 코드가 완성됐다. 

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step34_15649 {
    public static StringBuilder sb = new StringBuilder();
    public static int N, M;
    public static boolean[] check;
    public static int[] arr;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        
        check = new boolean[N];
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
            if (!check[i]) {
                check[i] = true;
                arr[depth] = i + 1;
                dfs(depth + 1);
                check[i] = false;
            }
        }
    }
}
```    

이번 문제에서는 boolean배열을 이용해서 내가 갔던 곳을 체크하는 걸 생각하지 못 해서 어려웠다.     
![image](https://user-images.githubusercontent.com/68698007/139520201-a2ee68d1-33e1-4593-8b12-93f194732930.png)
