---
title: 백준 10818(최대, 최소) - 1차원 배열
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/10818>
### N개의 정수가 주어진다. 이때, 최솟값과 최댓값을 구하는 프로그램을 작성하시오.
첫째 줄에 정수의 개수 N (1 ≤ N ≤ 1,000,000)이 주어진다. 둘째 줄에는 N개의 정수를 공백으로 구분해서 주어진다. 모든 정수는 -1,000,000보다 크거나 같고, 1,000,000보다 작거나 같은 정수이다.    
첫째 줄에 주어진 정수 N개의 최솟값과 최댓값을 공백으로 구분해 출력한다.    


N개의 정수가 주어지고 그 중에서 최소와 최대를 알아내야 된다.    
나는 Buffer를 이용해 정수를 받아들이므로 공백을 기준으로 받아들여진 정수들을 분리하기 위해 StringTokenizer를 사용할 것이고
배열을 이용한 방법, 이용하지 않아도 되는 방법으로 나눠서 풀이해봤다.

#### 1. 배열 이용
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

for문을 이용해 배열에 값을 저장하고 두 개의 if문을 둬서 max와 min을 찾아낸다.    
두 개의 if문인 이유는 입력에서 정수의 개수가 1개 이상이므로 만약 하나의 수만 입력된다면 min과 max 둘 다 
입력된 단 하나의 정수여야 되기 때문이다.    


#### 2. 배열, Arrays.sort()
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

while문을 이용해 배열에 값을 저장만 하고 Arrays.sort를 통해 정렬한 뒤 처음과 끝을 가져오는 것이다.    
Arrays.sort는 원시타입인 경우 DualPivotQuickSort.sort()를 불러온다. 이에대해서는 내가 조금 더 자세히 공부하고
따로 포스팅을 해야겠다. 알아야 될 것은 O(nlogn)을 기대할 수 있지만 최악의 경우에는 O(n^2)이라는 것이다.


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

사실 보면서도 굳이 배열을 둬야되나 싶었다. 문제에서 원하던건 배열이었으니 썼지만 그렇지 않다면 입력을 받는 즉시
비교하는 방법도 있다.    
변수를 하나 둬 StringTokenizer로 분리한 문자를 가져와 바로 min과 max로 비교하면 메모리 사용이 훨씬 적어질 것이다.    


![image](https://user-images.githubusercontent.com/68698007/133870078-92a00cf1-f669-4589-83b5-a4420337f67e.png)
1. 배열 X
2. 배열, Arrays.sort()
3. 배열


