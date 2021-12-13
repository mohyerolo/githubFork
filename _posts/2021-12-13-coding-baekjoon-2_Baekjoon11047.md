---
title: 백준 11047(동전 0) - 그리디 알고리즘
layout: post
categories: coding
tags: baekjoon
---
### 필요한 동전 개수의 최솟값을 구하는 프로그램을 작성하시오.
준규가 가지고 있는 동전은 총 N종류이고, 각각의 동전을 매우 많이 가지고 있다.
동전을 적절히 사용해서 그 가치의 합을 K로 만들려고 한다.    

첫째 줄에 N과 K가 주어진다. (1 ≤ N ≤ 10, 1 ≤ K ≤ 100,000,000)
둘째 줄부터 N개의 줄에 동전의 가치 Ai가 오름차순으로 주어진다. (1 ≤ Ai ≤ 1,000,000, A1 = 1, i ≥ 2인 경우에 Ai는 Ai-1의 배수)    

첫째 줄에 K원을 만드는데 필요한 동전 개수의 최솟값을 출력한다.    
<hr>

그리디 알고리즘 단계의 첫 번째 문제다.    

그리디 알고리즘은 __현재 시점에서 가장 이득이 되어 보이는 해를 선택하는 행위를 반복하는 알고리즘__ 으로 대부분의 경우 좋은 결과를 도출하지 못하지만 드물게 최적해를 보장하는 경우도 있다. 그리디 알고리즘은 최적화 문제를 대상으로 하고 이에는 최소 신장 트리, 최단 거리 등이 속한다(프림 알고리즘, 다익스트라 알고리즘).    

앞에서 풀었던 동적계획법(동적 프로그래밍)과 다른 점은 동적 프로그램은 최적의 해를 구하기는 하지만 그리디 알고리즘보다 덜 효율적이고, 그리디 알고리즘은 동적 프로그래밍보다 효율적이기는 하지만 DP처럼 반드시 최적의 해를 구해준다는 보장을 하지 못한다는 차이가 있다.    

<br>

이번 문제에서는 동전 개수의 최솟값을 출력해야되는 문제다. 그렇다면 우리는 우선 주어진 N개의 동전 중에서 K값을 만들 수 있는 가장 큰 값부터 나눠줘야된다는 걸 알 수 있다.    
N개의 동전은 오름차순으로 주어지므로 마지막 값부터 봐가면서 K보다 작다면 K를 동전 값으로 나눌 수 있는 횟수를 더해주고 K에서 값을 빼면 된다.    

<br>

#### 전체 코드
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step33_11047 {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());

        int[] coin = new int[N];

        for (int i = 0; i < N; i++) {
            coin[i] = Integer.parseInt(br.readLine());
        }

        int count = 0;
        for (int i = N - 1; i >= 0; i--) {
            if (coin[i] <= K) {
                count += (K / coin[i]);
                K = K % coin[i];
            }
        }
        System.out.println(count);
    }
}
```
