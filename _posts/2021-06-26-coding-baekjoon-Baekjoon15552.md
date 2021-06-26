---
title: 백준 15552(빠른 A + B)
layout: post
categories: coding
tags: baekjoon
---

<https://www.acmicpc.net/problem/15552>
### 각 테스트케이스마다 A+B를 한 줄에 하나씩 순서대로 출력한다.    
첫 줄에 테스트케이스의 개수 T가 주어진다. T는 최대 1,000,000이다. 다음 T줄에는 각각 두 정수 A와 B가 주어진다. A와 B는 1 이상, 1,000 이하이다.    
<hr>
최대 백만개의 케이스가 주어진다는 것이 중요하다. 문제에서부터 BufferedReader와 BufferedWriter를 사용해서
문제를 풀라고 제시해준다. Scanner와의 차이를 보여주기위한 문제인 것 같다.    
네가지 방법으로 풀어봤고 블로그에서 본 글을 참고해 나라면 생각하지 못 했을 방식으로도 풀어봤다.    
<br>

#### 1. BufferedReader, BufferedWriter
```java
package Step3;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.StringTokenizer;

public class Step3_15552_1 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int T = Integer.parseInt(br.readLine());
        StringTokenizer st;

        for (int i= 0; i < T; i++) {
            st = new StringTokenizer(br.readLine());
            bw.write((Integer.parseInt(st.nextToken()) + Integer.parseInt(st.nextToken())) + "\n"); 
        }
        br.close();
        bw.flush();
        bw.close();
    }
}
```    
문제에서 제시해준대로 BufferedReader와 BufferedWriter를 사용했다. BufferedReader로 입력받은 한 줄을 띄어쓰기를 기준으로 구분하기위해
StringTokenizer를 사용해 문자열을 분리했다.    


#### 2. BufferedReader, StringBuilder
```java
package Step3;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step3_15552_2 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int T = Integer.parseInt(br.readLine());
        StringTokenizer st;

        for (int i= 0; i < T; i++) {
            st = new StringTokenizer(br.readLine());
            sb.append(Integer.parseInt(st.nextToken()) + Integer.parseInt(st.nextToken())).append("\n");
        }
        br.close();
        System.out.println(sb);
    }
}
```    
BufferedWriter로 출력하는 대신 StringBuilder를 사용해봤다. 데이터 양이 지금보다 훨씬 더 많을 경우에는
BufferedWriter가 빠르다고는 하는데 현재는 StringBuilder가 약간 더 빨랐다.    


#### 3. BufferedReader, split()
```java
package Step3;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step3_15552_3 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int T = Integer.parseInt(br.readLine());
        String str;
        String[] arr;

        for (int i= 0; i < T; i++) {
            str = br.readLine();
            arr = str.split(" ");

            sb.append(Integer.parseInt(arr[0]) + Integer.parseInt(arr[1])).append("\n");
        }
        br.close();
        System.out.println(sb);
    }
}
```    
A + B에서 사용했던것처럼 여기서도 split을 사용해봤다. 데이터 양이 많은 경우에는 String.split()이 어떨지 궁금했다.    


#### 4. BufferedReader, subString()
```java
package Step3;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step3_15552_4{
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int T = Integer.parseInt(br.readLine());
        String str;

        for (int i= 0; i < T; i++) {
            str = br.readLine();
            int target = str.indexOf(" ");
            int result = Integer.parseInt(str.substring(0, target)) + Integer.parseInt(str.substring(target + 1));
            sb.append(result).append("\n");
        }
        br.close();
        System.out.println(sb);
    }
}
```     
subString으로 띄어쓰기가 있는 곳의 인덱스를 알아내 그걸 기준으로 문자를 분리한다.    
되게 성능 차이 많이 나는 걸 보고 깜짝 놀랐다.    

<br>
![image](https://user-images.githubusercontent.com/68698007/123502911-99da8d00-d68a-11eb-97c4-2b004d47391f.png)
1. subString
2. split
3. BufferedWriter
4. Stringbuilder
