---
title: 백준 2739(구구단)
layout: post
categories: coding
tags: baekjoon
comments: true
---
<https://www.acmicpc.net/problem/2739>
### N을 입력받은 뒤, 구구단 N단을 출력하는 프로그램을 작성하시오.   
첫째 줄에 N이 주어진다. N은 1보다 크거나 같고, 9보다 작거나 같다.
<hr>
처음 코딩을 배울때 꼭 해보는 구구단같다.    
이 간단한 구구단도 성능이라는 걸 비교해보려고 다섯번이나 시도해봤다. 다섯번 다 달랐다는 게 진짜 신기하다.    

#### 1. Scanner    
```java
import java.util.Scanner;

public class Step3_2739_1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();

        sc.close();

        for (int i = 1; i < 10; i++) {
            System.out.println(n + " * " + i + " = " + (n * i));
        }
    }
}
```    
Scanner를 사용해 입력받고 System.out으로 출력했다.    

#### 2. Scanner, BufferedWriter     
```java
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.OutputStreamWriter;
import java.util.Scanner;

public class Step3_2739_2 {
    public static void main(String[] args) throws IOException{
        Scanner sc = new Scanner(System.in);
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int n = sc.nextInt();
        sc.close();

        for (int i = 1; i < 10; i++) {
            bw.write(n + " * " + i + " = " + (n * i) + "\n");
        }
        bw.flush();
        bw.close();
    }
}
```    
Scanner로 입력, BufferedWriter로 출력했다.
입력에 비해 출력하는 횟수는 훨씬 많을테고 검사가 많을수록 System.out으로는 BufferedWriter보다 시간이 더 걸릴 것 같았다.    

#### 3. BufferedReader
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step3_2739_3 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        br.close();

        for (int i = 1; i < 10; i++) {
            System.out.println(n + " * " + i + " = " + (n * i));
        }
    }
}
```
BufferedReader로 입력, System.out으로 출력했다.
읽어들이는 건 Scanner에 비해 BufferedReader가 빠를테니 1번 보다는 속도가 훨씬 증가했을것이다.


#### 4. BufferedReader, BufferedWriter
```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class Step3_2739_4 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        
        int n = Integer.parseInt(br.readLine());
        br.close();

        for (int i = 1; i < 10; i++) {
            bw.write(n + " * " + i + " = " + (n * i) + "\n");
        }
        bw.flush();
        bw.close();
    }
}
```    
BufferedReader와 BufferedWriter를 사용했다. 입출력을 버퍼를 사용했으니 위에 세가지 경우보다 빠를 거라고 생각했는데 Buffer와 System.out.print로 출력한 것 보다 진짜 약간 느렸다...!!    

#### 5. BufferedReader, StringBuilder
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step3_2739_5 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        br.close();

        StringBuilder sb = new StringBuilder();

        for (int i = 1; i < 10; i++) {
            sb.append(n + " * " + i + " = " + (n * i) + "\n");
        }
        System.out.print(sb);
    }
}
```    
BufferedReader와 StringBuilder를 사용했다. StringBuilder로 객체를 만든 후 System.out.print로 출력하는 것과 BufferedWriter를 사용해 bw.write(sb.toString)로 출력하는 것에서 왜 버퍼 사용이
더 시간이 걸리는지는 약간 의문이다. toString과정과 버퍼 자원을 생성했다가 풀어주는 과정때문일까?    
    
    
구구단을 풀면서 java의 입출력들을 한 번 훑은 느낌이다. Scanner, BufferedReader, BufferedWrtier, StringBuilder까지... 참 많다~

![image](https://user-images.githubusercontent.com/68698007/122775759-6fcd4780-d2e5-11eb-97d5-5eab26af59e2.png)     
위에서부터 5번, 4번, 3, 2, 1이다.    
이번 문제에서는 BufferReader를 사용하냐 안 하냐의 유무가 시간을 줄이는거에 큰 영향을 끼치는 것으로 보인다. 나는 출력에서 더 시간이 줄어들 수 있을 거라고 생각했는데 이 문제에서는 생각보다 출력은 별로 영향이 없는 듯 하다. 
