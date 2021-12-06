---
title: 백준 1463(1로 만들기) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/1463>
### 정수 N이 주어졌을 때, 연산 세 개를 적절히 사용해서 1을 만들려고 한다. 연산을 사용하는 횟수의 최솟값을 출력하시오.
- X가 3으로 나누어 떨어지면, 3으로 나눈다.
- X가 2로 나누어 떨어지면, 2로 나눈다.
- 1을 뺀다.
     
첫째 줄에 1보다 크거나 같고, 106보다 작거나 같은 정수 N이 주어진다.    
<hr>
입려된 수를 1로 만들어야된다. 우리가 횟수를 저장할 배열 dp는 입력받은 수만큼을 잡으면 된다.    

그리고 숫자는 3으로 나누어 지거나, 2로 나누거나, 1을 빼거나, 6의 배수인 경우에 따라 dp 값을 수정해줘야한다.    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step16_1463 {
    public static int[] dp;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int N = Integer.parseInt(br.readLine());
        dp = new int[N + 1];

        for (int i = 0; i < dp.length; i++) {
            dp[i] = -1;
        }

        // 배열의 크기를 N + 1로 잡아서 0은 나오지 않는 수이고, 1이면 연산하지 않아도 되니까 0이 되는 것
        dp[0] = dp[1] = 0;
        System.out.println(count(N));
    }
}
```

재귀 함수인 count에서 우리는 N이 어떤 수로 나누어지는지를 알아야한다.    

1. 6으로 나누어진다면 연산 규칙에 들어가는 3과 2의 배수이므로 N을 3으로 나눈 연산 횟수, 2로 나눈 연산 횟수 중에 최소를 구하고 그 값을 N - 1의 연산 횟수와 비교해 최솟값  + 1을 dp에 저장
2. 3으로 나누어진다면 N / 3을 했을 때의 횟수와 N - 1을 했을 때를 비교해 최솟값을 가져오고 + 1을 해 저장
3. 2로 나누어진다면 N / 2를 했을 때의 횟수와 N - 1을 했을 때를 비교해 최솟값을 가져오고 + 1을 해 저장
4. 나누어지는 수가 아니라면 N - 1의 횟수를 가져와 1을 더해줌


```java
public static int count(int N) {
    if(dp[N] == -1) {
        if (N % 6 == 0) {
            dp[N] = Math.min(Math.min(count(N / 3), count(N / 2)), count(N - 1)) + 1;
        }
        else if (N % 3 == 0) {
            dp[N] = Math.min(count(N / 3), count(N - 1)) + 1;
        }
        else if (N % 2 == 0) {
            dp[N] = Math.min(count(N / 2), count(N - 1)) + 1;
        }
        else {
            dp[N] = count(N - 1) + 1;
        }
    }
    return dp[N];
}
```
<br>

#### 전체 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step16_1463 {
    public static int[] dp;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int N = Integer.parseInt(br.readLine());
        dp = new int[N + 1];

        for (int i = 0; i < dp.length; i++) {
            dp[i] = -1;
        }

        dp[0] = dp[1] = 0;
        System.out.println(count(N));
    }

    public static int count(int N) {
        if(dp[N] == -1) {
            if (N % 6 == 0) {
                dp[N] = Math.min(Math.min(count(N / 3), count(N / 2)), count(N - 1)) + 1;
            }
            else if (N % 3 == 0) {
                dp[N] = Math.min(count(N / 3), count(N - 1)) + 1;
            }
            else if (N % 2 == 0) {
                dp[N] = Math.min(count(N / 2), count(N - 1)) + 1;
            }
            else {
                dp[N] = count(N - 1) + 1;
            }
        }
        return dp[N];
    }
}
```
