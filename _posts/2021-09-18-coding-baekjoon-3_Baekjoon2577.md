---
title: 백준 2577(숫자의 개수) - 1차원 배열
layout: post
categories: coding
tags: baekjoon
---
### 세 개의 자연수 A, B, C가 주어질 때 A × B × C를 계산한 결과에 0부터 9까지 각각의 숫자가 몇 번씩 쓰였는지를 구하는 프로그램을 작성하시오.
예를 들어 A = 150, B = 266, C = 427 이라면 A × B × C = 150 × 266 × 427 = 17037300 이 되고, 계산한 결과 17037300 에는 0이 3번, 1이 1번, 3이 2번, 7이 2번 쓰였다.    
첫째 줄에 A, 둘째 줄에 B, 셋째 줄에 C가 주어진다. A, B, C는 모두 100보다 크거나 같고, 1,000보다 작은 자연수이다.    

0부터 9까지, 10개의 배열을 만들고 입력된 세 개의 수를 곱한 값의 자릿수를 살펴보며 각 수에 맞는 배열의 값을 증가시키면 된다.    

#### 1
```java
package Step6;

import java.io.*;

public class Step6_2577_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int mul = 1;
        int[] arr = new int[10];

        for (int i = 0; i < 3; i++) {
            mul *= Integer.parseInt(br.readLine());
        }

        String str = Integer.toString(mul);
        for (int i = 0; i < 10; i++) {
            for (int j = 0; j < str.length(); j++) {
                if ((str.charAt(j) - '0') == i) {
                    arr[i] += 1;
                }
            }
            sb.append(arr[i]).append("\n");
        }

        System.out.println(sb);
    }
}
```    


#### 2
```java
package Step6;

import java.io.*;

public class Step6_2577_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int mul = Integer.parseInt(br.readLine()) * Integer.parseInt(br.readLine()) * Integer.parseInt(br.readLine());
        int[] arr = new int[10];

        String str = Integer.toString(mul);

        for (int i = 0; i < str.length(); i++) {
            arr[(str.charAt(i) - '0')]++;
        }

        for (int a : arr) {
            sb.append(a).append("\n");
        }
        System.out.println(sb);
    }
}
```    

좀 더 간단하고 깔끔해보인다. 왜 나는 이런 생각을 한 번에 못 하는지...    
어차피 배열은 0으로 초기화가 되므로 그냥 자릿수만큼 반복하면서 있는 값만 채워주면 된다.    


#### 3
`` java
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int mul = Integer.parseInt(br.readLine()) * Integer.parseInt(br.readLine()) * Integer.parseInt(br.readLine());
        int[] arr = new int[10];

        while (mul != 0) {
            arr[mul % 10]++;
            mul /= 10;
        }

        for (int a : arr) {
            System.out.println(a);
        }
    }
}
```    

for문과 charAt를 사용하는 대신 while문과 %, /를 이용했다. 이게 더 간단하고 시간 안 걸릴것같은데


![image](https://user-images.githubusercontent.com/68698007/133870991-cbbb933a-acf0-4a37-8d94-3f8aab37401d.png)
1. while문
2. 2번
3. 1번

왜 while문이 시간이 좀 더 걸리는지는 잘 모르겠다. 숫자가 클 수록 연산하는게 charAt를 사용해 가져오는 것보다
오래걸리는것일까?
