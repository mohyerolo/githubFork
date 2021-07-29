---
title: 백준 10818 (최소, 최대) - 1차원 배열
layout: post
categoried: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/10818>
### N개의 정수가 주어진다. 이때, 최솟값과 최댓값을 구하는 프로그램을 작성하시오.
첫째 줄에 정수의 개수 N (1 ≤ N ≤ 1,000,000)이 주어진다. 둘째 줄에는 N개의 정수를 공백으로 구분해서 주어진다. 
모든 정수는 -1,000,000보다 크거나 같고, 1,000,000보다 작거나 같은 정수이다.
<hr>    

최소와 최대를 알아내는 문제로 백준에서는 1차원 배열을 이용하는 단계에 들어가는 문제이다.    
그런데 이번 문제에서는 사실 그렇게 배열을 이용할 필요가 없어보여서 배열을 이용하지 않은 풀이도 있다.

#### 1. 배열 O, if
```java
package Step6;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step6_10818_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int N = Integer.parseInt(br.readLine());
        int[] arr = new int[N];
        int min = 1000001;
        int max = -1000001;
        st = new StringTokenizer(br.readLine());

        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
            if (min > arr[i]) {
                min = arr[i];
            }
            if (max < arr[i]) {     // 정수의 개수가 1일때도 있으므로 else if가 아닌 그냥 if
                max = arr[i];
            }
        }

        System.out.println(min + " " + max);
    }
}
```    

min과 max값을 문제에서 설명한 최대와 최솟값으로 설정하고 StringTokenizer를 이용해 BufferedReader로 입력받은 문자를 구분한다 
구분한 문자들을 각각 arr이라는 배열에 집어넣고 배열에 있는 값을 현재 최소와 최댓값으로 비교한다.

if-else로 한 번만 비교하는 것이 아닌 주어진 정수의 값이 하나일수도있으니 if-if를 사용한다.


#### 2. 배열 O, Array.sort
```java
package Step6;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Step6_10818_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int N = Integer.parseInt(br.readLine());
        int[] arr = new int[N];
        st = new StringTokenizer(br.readLine());

        int i = 0;
        while (st.hasMoreTokens()) {
            arr[i++] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(arr);

        System.out.println(arr[0] + " " + arr[N - 1]);
    }
}
```   
java.util.Arrays 유틸리티 클래스의 sort() 메서드를 사용해 오름차순으로 정렬하는 방식을 사용했다. 
그러나 이런 정렬방식은 최악의 경우 시간복잡도가 O(n2)이기에 너무 많은 시간을 소요할 수 있다.


#### 3. 배열 X
```java
package Step6;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step6_10818_3 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int N = Integer.parseInt(br.readLine());
        int min = 1000001;
        int max = -1000001;
        st = new StringTokenizer(br.readLine());
        int a;

        for (int i = 0; i < N; i++) {
            a = Integer.parseInt(st.nextToken());
            if (min > a) {
                min = a;
            }
            if (max < a) {     // 정수의 개수가 1일때도 있으므로 else if가 아닌 그냥 if
                max = a;
            }
        }

        System.out.println(min + " " + max);
    }
}
```    

따로 배열에 저장한 것 없이 바로 비교하는 방식을 사용했다. 

<br>
![image](https://user-images.githubusercontent.com/68698007/127455203-34071373-9b9d-41f7-8cc8-b7bc0b3100cd.png)
1. 배열X
2. 배열, Arrays.sort
3. 배열, if

