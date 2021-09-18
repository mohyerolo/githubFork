---
title: 백준 1110(더하기 사이클) - while
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/1110>
### N이 주어졌을 때, N의 사이클의 길이를 구하는 프로그램을 작성하시오.
0보다 크거나 같고, 99보다 작거나 같은 정수가 주어질 때 다음과 같은 연산을 할 수 있다. 먼저 주어진 수가 10보다 작다면 앞에 0을 붙여 두 자리 수로 만들고, 각 자리의 숫자를 더한다.    
그 다음, 주어진 수의 가장 오른쪽 자리 수와 앞에서 구한 합의 가장 오른쪽 자리 수를 이어 붙이면 새로운 수를 만들 수 있다. 다음 예를 보자.    
26부터 시작한다. 2+6 = 8이다. 새로운 수는 68이다. 6+8 = 14이다. 새로운 수는 84이다. 8+4 = 12이다. 새로운 수는 42이다. 4+2 = 6이다. 새로운 수는 26이다.    
위의 예는 4번만에 원래 수로 돌아올 수 있다. 따라서 26의 사이클의 길이는 4이다.    

두 자리가 최대라는 것이므로 10의 자리, 1의 자리를 가지는 변수를 두면 된다.    
/와 %를 사용해 각각의 수를 구해낸다. /를 통해 구해지는 수는 10의 자리 수고 %는 일의 자리 수를 구해주므로
두 개의 합을 구한 다음 전에 구한 일의 자리수에 10을 곱하고 합을 다시 % 10 하여 일의 자리 수를 빼내는 식으로 
반복하면 된다.

#### BufferedReader
``` java
package Step2;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step2_1110_1 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        int n = Integer.parseInt(br.readLine());
        int A = n / 10;
        int B = n % 10;
        int sum = A + B;
        int c = 1;

        while ((B * 10 + (sum % 10)) != n) {
            A = B;
            B = sum % 10;
            sum = A + B;
            c++;
        }

        System.out.println(c);
    }
}    
```
