---
title: 백준 1003(피보나치 함수) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/1003>
### N이 주어졌을 때, fibonacci(N)을 호출했을 때, 0과 1이 각각 몇 번 출력되는지 구하는 프로그램을 작성하시오.
첫째 줄에 테스트 케이스의 개수 T가 주어진다.

각 테스트 케이스는 한 줄로 이루어져 있고, N이 주어진다. N은 40보다 작거나 같은 자연수 또는 0이다.    

각 테스트 케이스마다 0이 출력되는 횟수와 1이 출력되는 횟수를 공백으로 구분해서 출력한다.
<hr>
동적 계획법은 학교에서 c언어로 배운적이 있어서 어떻게 하는지는 알았다. 분명 과제로 제출한 적도 있는 것 같은데 이제는 기억도 안 나는 magic..

<https://st-lab.tistory.com/124>    
결국은 또 이 블로그를 보고 풀 수밖에 없었다.    

동적 계획법은 재귀와 연관있다. 복잡한 문제를 간단한 여러 개의 문제로 나누어 푸는 방법으로 각 문제의 값을 저장해서 좀 더 큰 문제에 저장된 값을 가져와 풀게되는 것이다. 즉, 가능한 모든 방법을 고려하게 된다.    

이번 문제에서는 피보나치 값을 구하는 게 아닌 피보나치 값을 구하는 과정에서 0과 1이 몇 번 계산되는지를 구하는 것이다.    

0과 1은 각각 fibo(0), fibo(1)의 값으로 결국 문제는 피보나치 값을 구하는 과정에서 fibo(0)과 fibo(1)을 몇 번 호출하느냐를 알아내는 것이다.    

<br>

0과 1의 값을 담을 이차원 배열을 만들어야 된다. 개수가 40보다 작거나 같으므로 [41][2]로 만들면 된다. 40으로 할 수도 있지만 좀 더 직관적으로 알 수 있게 41로 만든것이다.     
그리고 우리는 fibo(0)에서는 0이, fibo(1)에서는 1이 한 번 호출된다는 것을 아니까 dp[0]과 dp[1]의 값을 각각 설정해준다.    
이렇게 초기값을 하나라도 설정해줘야 재귀를 할 때 참고할 값이 하나라도 생겨서 정상적으로 작동하는 것이다.    


```java
public class Step16_1003 {
    public static Integer[][] dp = new Integer[41][2];

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        dp[0][0] = 1;
        dp[0][1] = 0;
        dp[1][0] = 0;
        dp[1][1] = 1;

        int T = Integer.parseInt(br.readLine());
        for (int i = 0; i < T; i++) {
            int N = Integer.parseInt(br.readLine());
            fibo(N);
            sb.append(dp[N][0]).append(' ').append(dp[N][1]).append('\n');
        }

        System.out.println(sb);
    }
}
```

그러면 우리는 이제 재귀에 들어갈 함수를 작성해야 한다.    
Fibo(3) = Fibo(2) + (1)이다.    

Fibo(2) = Fibo(1) + Fibo(0)으로 결국 Fibo(3) = {Fibo(1) + Fibo(0)} + Fibo(1)이 된다.    

Fibo(4) = Fibo(3) + Fibo(2) = {Fibo(2) + Fibo(1)} + {Fibo(1) + Fibo(0)} = {{Fibo(1) + Fibo(0)} + Fibo(1)} + {Fibo(1) + Fibo(0)}이 된다.    

이는 결국, Fibo[N]의 0과 1의 호출은 <mark style='background-color: #fff5b1'>Fibo[N - 1]의 0과 1의 호출 + Fibo[N - 2]의 0과 1 호출 개수</mark>가 된다는 것이다. 이를 재귀적으로 풀이하면

```java
if (dp[n][0] == null || dp[n][1] == null) {
    dp[n][0] = fibo(n - 1)[0] + fibo(n - 2)[0];
    dp[n][1] = fibo(n - 1)[1] + fibo(n - 2)[1];
}
```
이렇게 된다.    

dp[n][0] == null이라는 것은 Integer타입으로 선언을 해서 그렇다. int형 배열은 자동으로 0이 들어가지만 Integer형은 null로 선언이 되어 입력된 값이 있지 않으면 null로 체크를 할 수 있다.    

그래서 만약 우리가 구하고자하는 피보나치의 값이 아직 구해지지 않았다면 n-1과 n-2의 값을 참고해서 구할 수 있는 것이다.

그런데 우리는 재귀를 호출할때 모든 이차원 배열이 아닌 Fibo(N)에서 N만 알면 되므로 재귀의 반환 타입은 Integer[]가 된다.    
<br>

```java
public static Integer[] fibo(int n) {
        if (dp[n][0] == null || dp[n][1] == null) {
            dp[n][0] = fibo(n - 1)[0] + fibo(n - 2)[0];
            dp[n][1] = fibo(n - 1)[1] + fibo(n - 2)[1];
        }
        return dp[n];
    }
```

### 전체코드    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step16_1003 {
    public static Integer[][] dp = new Integer[41][2];

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        dp[0][0] = 1;
        dp[0][1] = 0;
        dp[1][0] = 0;
        dp[1][1] = 1;

        int T = Integer.parseInt(br.readLine());
        for (int i = 0; i < T; i++) {
            int N = Integer.parseInt(br.readLine());
            fibo(N);
            sb.append(dp[N][0]).append(' ').append(dp[N][1]).append('\n');
        }

        System.out.println(sb);
    }

    public static Integer[] fibo(int n) {
        if (dp[n][0] == null || dp[n][1] == null) {
            dp[n][0] = fibo(n - 1)[0] + fibo(n - 2)[0];
            dp[n][1] = fibo(n - 1)[1] + fibo(n - 2)[1];
        }
        return dp[n];
    }
}
```
