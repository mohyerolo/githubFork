---
title: 백준 1904(01타일) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/1904>
### N이 주어졌을 때 만들 수 있는 모든 가짓수를 출력하시오.
현재 1 하나만으로 이루어진 타일 또는 0타일을 두 개 붙인 한 쌍의 00타일들만이 남게 되었다.    
N=1일 때 1만 만들 수 있고, N=2일 때는 00, 11을 만들 수 있다. (01, 10은 만들 수 없게 되었다.) 또한 N=4일 때는 0011, 0000, 1001, 1100, 1111 등 총 5개의 2진 수열을 만들 수 있다.    

첫 번째 줄에 자연수 N이 주어진다. (1 ≤ N ≤ 1,000,000)    
첫 번째 줄에 지원이가 만들 수 있는 길이가 N인 모든 2진 수열의 개수를 15746으로 나눈 나머지를 출력한다.
<hr>
00과 1로 만들 수 있는 개수를 구하는 문제다.    

자연수 N이 1부터 1,000,000까지 가능하므로 int형 배열의 크기는 1000001로 정한다.    
    
우리는 N = 1일 때 1개, 2일 때 2개라는 걸 알고있으므로 배열 dp[1], dp[2] 값을 1, 2로 정할 수 있다.    

int형 배열로 사용하므로 0으로 초기화됐을 원소 값을 전부 -1로 해주는 과정이 필요하다.    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step16_1904_2 {
    public static int[] dp = new int[1000001];

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;

        for (int i = 3; i < dp.length; i++) {
            dp[i] = -1;
        }

        System.out.println(Tile(N));
    }
}
```

재귀를 만들어보도록 하자.    
N = 1일 때 1만 가능 -> 1개    
N = 2일 때 00, 11 -> 2개    
N = 3일 때 001, 100, 111 -> 3개    
N = 4일 때 0011, 0000,1001, 1100, 1111 -> 5개    
N = 5일 때 00001, 00100, 00111, 10000, 10011, 11001, 11100, 11111 -> 8개    

마치 피보나치처럼 N에서 나오는 값이 N  - 1의 값 + N - 2의 값인 걸 볼 수 있다. 

즉, Tile 재귀 함수는

```java
public static int Tile(int n) {
    if (dp[n] == -1) {
        dp[n] = (Tile(n - 1) + Tile(n - 2)) % 15746;
    }
    return dp[n];
}
```
이런 모습을 갖추게 된다.    
<br>

### 전체코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step16_1904_2 {
    public static int[] dp = new int[1000001];

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;

        for (int i = 3; i < dp.length; i++) {
            dp[i] = -1;
        }

        System.out.println(Tile(N));
    }

    public static int Tile(int n) {
        if (dp[n] == -1) {
            dp[n] = (Tile(n - 1) + Tile(n - 2)) % 15746;
        }
        return dp[n];
    }
}
```
