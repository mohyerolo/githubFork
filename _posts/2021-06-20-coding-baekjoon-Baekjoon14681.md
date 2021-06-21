---
title: 백준 14681(사분면 고르기)
categories: coding
tags: baekjoon
comments: true
layout: post
---
<https://www.acmicpc.net/problem/14681>
### 점의 좌표를 입력받아 그 점이 어느 사분면에 속하는지 알아내는 프로그램을 작성하시오.    
단, x좌표와 y좌표는 모두 양수나 음수라고 가정한다.    
<hr>

그렇게 어렵지 않은 문제였다. 역시 Scanner와 Buffer를 이용해 두 번 풀어봤다.    

#### 1. Scanner
```java
import java.util.Scanner;

public class Step4_14681_1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int x = sc.nextInt();
        int y = sc.nextInt();

        sc.close();

        if (x > 0) {
            if (y > 0) {
                System.out.println("1");
            }
            else {
                System.out.println("4");
            }
        }
        else {
            if (y > 0) {
                System.out.println("2");
            }
            else {
                System.out.println("3");
            }
        }
    }
}
```    

#### 2. Buffer
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step4_14681_2 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        int x = Integer.parseInt(br.readLine());
        int y = Integer.parseInt(br.readLine());

        if (x > 0) {
            if (y > 0) {
                System.out.println("1");
            }
            else {
                System.out.println("4");
            }
        }
        else {
            if (y > 0) {
                System.out.println("2");
            }
            else {
                System.out.println("3");
            }
        }
    }
}
```    

사실 두 개 성능이 뭐 달라봤자 얼마나 다를까 싶었다.    

![image](https://user-images.githubusercontent.com/68698007/122772603-832ae380-d2e2-11eb-9a05-4b58f7b42e8b.png)
1. BufferedReader
2. Scanner    

생각보다 시간에서는 차이가 있었다.
