---
title: 백준 12865(평범한 배낭) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/12865>
### 배낭에 넣을 수 있는 물건들의 가치의 최댓값을 알려주자
준서가 여행에 필요하다고 생각하는 N개의 물건이 있다. 각 물건은 무게 W와 가치 V를 가지는데, 해당 물건을 배낭에 넣어서 가면 준서가 V만큼 즐길 수 있다. 아직 행군을 해본 적이 없는 준서는 최대 K만큼의 무게만을 넣을 수 있는 배낭만 들고 다닐 수 있다.    

첫 줄에 물품의 수 N(1 ≤ N ≤ 100)과 준서가 버틸 수 있는 무게 K(1 ≤ K ≤ 100,000)가 주어진다. 두 번째 줄부터 N개의 줄에 거쳐 각 물건의 무게 W(1 ≤ W ≤ 100,000)와 해당 물건의 가치 V(0 ≤ V ≤ 1,000)가 주어진다. 입력으로 주어지는 모든 수는 정수이다.     

한 줄에 배낭에 넣을 수 있는 물건들의 가치합의 최댓값을 출력한다.    
<hr>

무게와 가치가 주어지고 배낭에 넣을 수 있는 최댓값 이하로 물건을 넣어 합이 최대가 되도록 고르는 방법을 찾는 문제다. 이런 문제는 __냅색(knapsack)문제__ 라고 하며 냅색 알고리즘은 크게 두 가지, 짐을 쪼갤 수 있는 경우(Fraction Knapsack)와 짐을 쪼개지 못하는 경우(0/1 Knapsack)로 나눠진다. 전자의 경우 그리디 알고리즘을 통해 풀 수 있지만 후자의 경우에는 DP를 사용해 풀 수 있다.    

이번 문제는 후자의 경우로 정해진 무게를 넣을 수 있는 배낭이 정해져있고 짐을 쪼갤 수 없으니 DP를 사용해 풀어야 한다.    
<br>

이번에 사용될 dp배열의 각 인덱스는 dp[i번째 아이템][무게]를 의미한다.    
예시로 주어진 (6, 13), (4, 8), (3, 6), (5, 12)에서 첫번째 아이템의 경우 무게가 6이므로 {0, 0, 0, 0, 0, 13, 13}이 dp[0]에 담기는거다.    

두 번째 아이템의 경우는 {0, 0, 0, 8, 8}를 가지고 있다가 무게가 6일때부터 달라진다. 만약 두 번째 아이템을 지니면서 첫 번째 아이템도 가지게 된다면 정해진 무게 7을 넘게된다. 그래서 두 가지 아이템을 다 갖지 못 하지만 두 번째 아이템이 아닌 첫 번째 아이템만 가지고 있는 게 훨씬 높은 가치를 지닐 수 있다. 그래서 결국 dp[1]은 {0, 0, 0, 8, 8, 13, 13}이 된다. dp는 결국 현재까지 가능한 아이템들중에서 1부터 K까지의 무게가 있을 때 어떤 값이 최대인지를 저장하는것이다.    

결국 예제에서 사용된 dp의 모습은 최종적으로 아래가 되겠다.    
{0, 0, 0, 0, 0, 13, 13}    
{0, 0, 0, 8, 8, 13, 13}    
{0, 0, 6, 8, 8, 13, 14} &nbsp; &nbsp;- 무게가 7일때: 무게 3 + 무게 4    
{0, 0, 6, 8, 12, 13, 14}    
    
<br>

dp의 모습을 보면 dp[1][2]은 dp[0][2]의 값을 갖고, dp[3][2]는 dp[2][2]의 값을 갖는다. 그러나 자기의 아이템이 배낭에 들어갈 수 있어질때는 내 아이템이 들어감으로써 변경되는 가치와 이미 이전에 저장된 가치(dp[i - 1][j])를 비교해야된다. 내 아이템이 들어가서 변경되는 가치는 __내 아이템의 가치 + 이전 아이템에서 현재 내 무게를 뺀만큼의 무게의 가치__ 가 된다. 즉 d[i][j] = dp[i - 1][j - w[i]] + v[i]인것이다.    

#### 전체 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

// https://www.acmicpc.net/problem/12865
public class Step16_12865 {
    public static Integer[][] dp;
    public static int[] w;
    public static int[] v;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());

        w = new int[N];
        v = new int[N];
        dp = new Integer[N][K + 1];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            w[i] = Integer.parseInt(st.nextToken());
            v[i] = Integer.parseInt(st.nextToken());
        }

        System.out.println(knapscak(N - 1, K));
    }

    public static int knapscak(int i, int k) {
        if (i < 0) {
            return 0;
        }
        if (dp[i][k] == null) {
            if (w[i] > k) {
                dp[i][k] = knapscak(i - 1, k);
            }
            else {
                dp[i][k] = Math.max(knapscak(i - 1, k), knapscak(i - 1, k - w[i]) + v[i]);
            }
        }

        return dp[i][k];
    }
}  
```
