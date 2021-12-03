---
title: 백준 9184(신나는 함수 실행) - 동적 계획법 1
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/9184>
### a, b, c가 주어졌을 때, w(a, b, c)를 출력하는 프로그램을 작성하시오.
입력은 세 정수 a, b, c로 이루어져 있으며, 한 줄에 하나씩 주어진다. 입력의 마지막은 -1 -1 -1로 나타내며, 세 정수가 모두 -1인 경우는 입력의 마지막을 제외하면 없다.    
<hr>
재귀함수를 문제에서 주어주고 그거에 맞춰 내가 동적계획법으로 푸는 방법을 작성하면 된다.    

주어진 재귀함수는 아래와 같다.
```
if a <= 0 or b <= 0 or c <= 0, then w(a, b, c) returns:
    1

if a > 20 or b > 20 or c > 20, then w(a, b, c) returns:
    w(20, 20, 20)

if a < b and b < c, then w(a, b, c) returns:
    w(a, b, c-1) + w(a, b-1, c-1) - w(a, b-1, c)

otherwise it returns:
    w(a-1, b, c) + w(a-1, b-1, c) + w(a-1, b, c-1) - w(a-1, b-1, c-1)
```

- a, b, c중 하나라도 0이하라면 1 리턴
- 셋 중 하나라도 20이상이라면 w(20, 20, 20)
- a < b이고 b < c면 w(a, b, c-1) + w(a, b-1, c-1) - w(a, b-1, c)
- 그 외의 경우에는 w(a-1, b, c) + w(a-1, b-1, c) + w(a-1, b, c-1) - w(a-1, b-1, c-1)

네 가지의 조건이 주어졌다.    

__어떤 수든 0이하면 1, 20이상이면 w(20, 20, 20)을 호출하므로 배열은 20까지만 있으면 된다.__ 그러므로 각 a,b,c에 따른 값을 갖게 될 int[21][21][21]을 선언하면 된다. (20으로 선언해도 되지만 직관적으로 보기 편하기 위해 21로 한 것)

또한 세 정수가 모두 -1인 경우가 입력의 마지막이므로 while문을 이용해 세 개의 값을 검사하며 진행하도록 해야한다.    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step16_9184 {
    public static int[][][] dp = new int[21][21][21];
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();
        int a, b, c;

        while (true) {
            st = new StringTokenizer(br.readLine());
            a = Integer.parseInt(st.nextToken());
            b = Integer.parseInt(st.nextToken());
            c = Integer.parseInt(st.nextToken());
            
            if (a == -1 && b == -1 && c == -1) {
                break;
            }

            sb.append("w(").append(a).append(", ").append(b)
            .append(", ").append(c).append(") = ").append(w(a, b, c)).append('\n');
        }
        System.out.println(sb);
    }
}
```

그렇다면 이제 주어진 조건에 맞는 동적계획법을 이용한 재귀함수를 작성해야한다.    
우리가 재귀를 생각하지 않아도 되니까 좀 편하기는 했다.

```java
public static int w(int a, int b, int c) {
        if (a <= 0 || b <= 0 || c <= 0) {
            return 1;
        }

        if (a > 20 || b > 20 || c > 20) {
            return dp[20][20][20] = w(20, 20, 20);
        }

        if (dp[a][b][c] != 0) {
            return dp[a][b][c];
        }

        if (a < b && b < c) {
            return dp[a][b][c] = w(a, b, c - 1) + w(a, b - 1, c -1) - w(a, b - 1, c);
        }
        
        return dp[a][b][c] = w(a-1, b, c) + w(a-1, b-1, c) + w(a-1, b, c-1) - w(a-1, b-1, c-1);
    }
```
if (a > 20 || b > 20 || c > 20)에서 만약 dp[20][20][20]의 값이 있다면 w(20, 20, 20)을 호출하지 않고 바로 값을 리턴하면 되니까

```java
if (a > 20 || b > 20 || c > 20) {
    if (dp[20][20][20] != null) {
        return dp[20][20][20];
    }
    return dp[20][20][20] = w(20, 20, 20);
}
```
이렇게도 작성을 했었는데 전 것과 시간 차이는 어차피 많이 나지도 않는 걸 보고 지저분해보여서 그냥 뺐다.    


### 전체 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step16_9184 {
    public static int[][][] dp = new int[21][21][21];
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();
        int a, b, c;

        while (true) {
            st = new StringTokenizer(br.readLine());
            a = Integer.parseInt(st.nextToken());
            b = Integer.parseInt(st.nextToken());
            c = Integer.parseInt(st.nextToken());
            
            if (a == -1 && b == -1 && c == -1) {
                break;
            }

            sb.append("w(").append(a).append(", ").append(b)
            .append(", ").append(c).append(") = ").append(w(a, b, c)).append('\n');
        }
        System.out.println(sb);
    }

    public static int w(int a, int b, int c) {
        if (a <= 0 || b <= 0 || c <= 0) {
            return 1;
        }

        if (a > 20 || b > 20 || c > 20) {
            return dp[20][20][20] = w(20, 20, 20);
        }

        if (dp[a][b][c] != 0) {
            return dp[a][b][c];
        }

        if (a < b && b < c) {
            return dp[a][b][c] = w(a, b, c - 1) + w(a, b - 1, c -1) - w(a, b - 1, c);
        }
        
        return dp[a][b][c] = w(a-1, b, c) + w(a-1, b-1, c) + w(a-1, b, c-1) - w(a-1, b-1, c-1);
    }
}
```
