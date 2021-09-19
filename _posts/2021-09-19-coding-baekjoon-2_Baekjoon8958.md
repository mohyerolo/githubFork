---
title: 백준 8958(OX퀴즈) - 1차원 배열
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/8958>

### "OOXXOXXOOO"와 같은 OX퀴즈의 결과가 있다. O는 문제를 맞은 것이고, X는 문제를 틀린 것이다. 문제를 맞은 경우 그 문제의 점수는 그 문제까지 연속된 O의 개수가 된다. 예를 들어, 10번 문제의 점수는 3이 된다. OX퀴즈의 결과가 주어졌을 때, 점수를 구하는 프로그램을 작성하시오.
첫째 줄에 테스트 케이스의 개수가 주어진다. 각 테스트 케이스는 한 줄로 이루어져 있고, 길이가 0보다 크고 80보다 작은 문자열이 주어진다. 문자열은 O와 X만으로 이루어져 있다.    
각 테스트 케이스마다 점수를 출력한다.    

문자열이 반복되는지를 보면 된다. 그리 어렵지는 않으나 byte를 사용하면 간단할 수 있다는 걸 알게 된 문제다.    

#### 1. 배열, charAt()
```java
package Step6;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step6_8958_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] str = new String[Integer.parseInt(br.readLine())];
        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < str.length; i++) {
            str[i] = br.readLine();
        }

        int cnt;
        int sum;
        for (int i = 0; i < str.length; i++) {
            cnt = 0;
            sum = 0;
            for (int j = 0; j < str[i].length(); j++) {
                if (str[i].charAt(j) == 'O') {
                    cnt++;
                    sum += cnt;
                }
                else {
                    cnt = 0;
                }
            }

            sb.append(sum).append("\n");
        }

        System.out.print(sb);
    }
}
```    

String배열로 각 테스트 케이스를 받아온다. 첫 번째 for문에서는 테스트 케이스를 순회하는 것이고 두 번째 for문에서 하나의 테스트 케이스를 살펴본다.    
하나의 문자열의 문자를 charAt로 꺼내와 만약 'O'라면 cnt를 늘려주고 sum에 값을 더해주지만 'X'가 나오면 cnt를 0으로 초기화하는 것이다.    


#### 2. 배열 X, getBytes()
```java
package Step6;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step6_8958_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());
        for (int i = 0; i < n; i++) {
            int cnt = 0;
            int sum = 0;
            for (byte value : br.readLine().getBytes()) {
                if (value == 'O') {
                    cnt++;
                    sum += cnt;
                }
                else {
                    cnt = 0;
                }
            }

            sb.append(sum).append("\n");
        }

        System.out.print(sb);
    }
}
```    

배열을 이용하지 않고 입력을 그때마다 받아오도록 한다. getBytes()는 String의 메소드로 byte 배열을 반환한다.    
br.readLine()으로 읽어온 한 줄을 byte 배열로 가져오는 것으로 문자 하나 하나를 배열로 담아오는 것이다. 그래서 for-each로 반복하는 것이 가능하다.    
가져온 byte값을 확인해주기만 하면 된다.    
이럴 경우 따로 메소드를 사용하지 않아도 문자 하나하나에 접근이 가능하다.    


![image](https://user-images.githubusercontent.com/68698007/133923556-e5efc3c2-33be-40b4-ba56-83cb2dfe8207.png)
1. 배열 X, getBytes()
2. 배열 O, charAt()
