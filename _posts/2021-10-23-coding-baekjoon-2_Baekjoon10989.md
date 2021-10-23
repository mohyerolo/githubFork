---
title: 백준 10989(수 정렬 3) - 정렬
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/10989>
### N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.
첫째 줄에 수의 개수 N(1 ≤ N ≤ 10,000,000)이 주어진다. 둘째 줄부터 N개의 줄에는 수가 주어진다. 이 수는 10,000보다 작거나 같은 자연수이다.
<hr>
지금까지와 똑같은 수 정렬이지만 수의 개수는 천만개이고 수가 중복되지 않는다는 얘기가 빠져있다.    
그러나 수가 10,000보다 작거나 같은 자연수이므로 수정렬, 수정렬2보다 범위는 훨씬 작다.    

지금까지와 같이 봤던 정렬중에 계수 정렬을 사용하면 되는 것이다.

#### Counting Sort
```java
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());
        int[] counting = new int[10001];

        for (int i = 0; i < n; i++) {
            counting[Integer.parseInt(br.readLine())]++;
        }

        for (int i = 1; i < counting.length; i++) {
            while (counting[i] > 0) {
                sb.append(i).append('\n');
                counting[i]--;
            }
        }

        System.out.println(sb);
    }
}
```    
저번과는 다르게 배열을 int형으로 선언했다. 전까지는 중복되는 수가 없었으므로 굳이 int로 할 필요가 없었으나 이번에는 중복이 가능하므로 int로 수의 개수를 세야한다.    

이걸로 Counting Sort에 대해서는 꽤 잘 알고 지나가는 것 같다.
