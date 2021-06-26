---
title: 백준 2741(N찍기)
layout: post
categories: coding
tags: baekjoon
---

<https://www.acmicpc.net/problem/2741>
### 자연수 N이 주어졌을 때, 1부터 N까지 한 줄에 하나씩 출력하는 프로그램을 작성하시오.
첫째 줄에 100,000보다 작거나 같은 자연수 N이 주어진다. 첫째 줄부터 N번째 줄 까지 차례대로 출력한다.    
<hr>
10만보다 작지만 출력이 10만개가 될 수 있다는 얘기이므로 출력에 BufferedWriter와 StringBuilder를 이용했다.    

<br>
#### 1. BufferedWriter

```java
package Step3;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class Step3_2741_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int n = Integer.parseInt(br.readLine());

        br.close();
        
        for (int i = 1; i <= n; i++) {
            bw.write(i + "\n");
        }

        bw.flush();
        bw.close();
    
    }
}
```    
bw.write를 통해 1부터 버퍼에 저장을 하고 flush로 내보낸다.    
<br>

#### 2. StringBuilder
```java
package Step3;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step3_2741_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int N = Integer.parseInt(br.readLine());
        br.close();
        
        for (int i = 1; i <= N; i++) {
            sb.append(i).append("\n");
        }
        System.out.println(sb);
    }
}
```     

<br>
![image](https://user-images.githubusercontent.com/68698007/123503806-40755c80-d690-11eb-951e-c80e38ec3dbd.png)
1. BufferedWriter
2. StringBuilder

