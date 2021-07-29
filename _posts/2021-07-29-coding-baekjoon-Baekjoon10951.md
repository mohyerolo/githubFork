---
title: 백준 10951(A + B - 4) - while
layout: post
categories: coding
tags: baekjoon
comments: false
---

<https://www.acmicpc.net/problem/10951>
### 두 정수 A와 B를 입력받은 다음, A+B를 출력하는 프로그램을 작성하시오.
입력은 여러 개의 테스트 케이스로 이루어져 있다.
각 테스트 케이스는 한 줄로 이루어져 있으며, 각 줄에 A와 B가 주어진다. (0 < A, B < 10)
<hr>

입력의 종료를 더이상 읽을 수 있는 데이터 (EOF)로 판단하는 것이 중요하다.
EOF에 대해서는 따로 올릴 것이고 우선은 문제 풀이부터 해보겠다.

Scanner와 BufferedReader를 이용한 풀이가 있겠지만 나는 BufferedReader로만 풀어봤다.

#### BufferedReader
```java
package Step2;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step2_10951_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        
        int A = 0;
        int B = 0;
        String str;

        while ((str = br.readLine()) != null) {
            A = str.charAt(0) - '0';
            B = str.charAt(2) - '0';
            sb.append(A + B).append("\n");
        }
        
        System.out.println(sb);
        br.close();
    } 
}
```    
BufferedReader로 읽어온 문자열이 null일 경우로 검사해 파일의 끝을 알아낸다.    


