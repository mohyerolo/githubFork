---
title: 백준 10844(쉬운 계단 수) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/10844>
### N이 주어질 때, 길이가 N인 계단 수가 총 몇 개 있는지 구해보자
45656이란 수를 보자.    
이 수는 인접한 모든 자리의 차이가 1이다. 이런 수를 계단 수라고 한다.    

첫째 줄에 N이 주어진다. N은 1보다 크거나 같고, 100보다 작거나 같은 자연수이다.    
첫째 줄에 정답을 1,000,000,000으로 나눈 나머지를 출력한다.
<hr>
처음에 이 문제를 봤을 때 아무리봐도 예시로 알려 준 45656이라는 수가 계단 수라고 하는 것 까지는 알겠는데 예제 입력인 1에 왜 9가 출력되는지는 이해할 수가 없었다.    

길이가 1인 계단 수라는게 도대체 무엇인지 알 수 없어 문제에 질문해주신 분들에게 달린 답을 보고 겨우 이해가 가능했다.    

길이가 1인 계단 수에는 1, 2, 3, 4, 5, 6, 7, 8, 9가 들어간다. 10이면 길이가 2인 계단 수가 되는 것이다.     
길이가 2인 계단 수에는 {10, 12, 21, 23, 32, 34, 43,..., 98}까지로 17개가 나온다.    
길이가 3인 계단 수에는 {101, 121, 123, 210, 212, 232, 234,...}등이다.

<br>

길이가 3, 앞에가 1일 때는 순서대로 한 개, 두 개, 세 개로 증가한다. 
__1 다음에는 0, 2 가능__
- 0일 경우: 길이가 2임. 그러나 그 다음으로는 1만 가능. 1반환
- 2일 경우: 길이가 2. 그 다음으로 1, 3 가능
    - 1일 경우: 길이가 1. 1반환
    - 3일 경우: 길이가 1. 1반환
    - 두 개를 더한 2 반환
- 두 개를 더한 3이 길이가 3이고 앞이 1일 때 가능한 개수

앞에가 2일 때는 순서대로 한 개, 두 개, 네 개로 증가한다. 
__2 다음에는 1, 3 가능__
- 1일 경우: 길이가 2. 다음으로 0, 2 가능
    - 0일 경우: 길이 1. 1반환
    - 2일 경우: 길이 1. 1반환
    - 두 개를 더한 2반환
- 3일 경우: 길이 2. 다음으로 2, 4 가능
    - 2일 경우: 길이 1. 1반환
    - 4일 경우: 길이 1. 1반환
    - 두 개를 더한 2 반환
- 1과 3일 경우를 더한 4 반환. 길이 3에 앞이 2일 경우 가능한 개수 = 4


이런 식으로 몇 개가 있는지를 구할 수 있다.

#### 전체 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step16_preveiw {
    public static Long[][] dp;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        dp = new Long[N + 1][10];
        
        // 길이가 1일때를 설정해주는 것
        for (int i = 0; i < 10; i++) {
            dp[1][i] = 1L;
        }

        int result = 0;
        // 길이가 N일때 첫번째 자리가 1부터 9일때 각각 몇개가 있는지
        for (int i = 1; i < 10; i++) {
            result += count(N, i);
        }
        
    }

    public static Long count(int depth, int val) {
        if (depth == 1) return dp[depth][val];
        if (dp[depth][val] == null) {
            if (val == 0) {
                dp[depth][val] = count(depth - 1, 1);
            }
            else if (val == 9) {
                dp[depth][val] = count(depth - 1, 8);
            }
            else {
                dp[depth][val] = count(depth - 1, val - 1) + count(depth - 1, val + 1);
            }
        }
        return dp[depth][val] %  1000000000;
    }
}
```
