---
title: 백준 4344(평균은 넘겠지) - 1차원 배열
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/4344>
### 각 케이스마다 한 줄씩 평균을 넘는 학생들의 비율을 반올림하여 소수점 셋째 자리까지 출력한다.
첫째 줄에는 테스트 케이스의 개수 C가 주어진다.    
둘째 줄부터 각 테스트 케이스마다 학생의 수 N(1 ≤ N ≤ 1000, N은 정수)이 첫 수로 주어지고, 이어서 N명의 점수가 주어진다. 점수는 0보다 크거나 같고, 100보다 작거나 같은 정수이다.    

테이트 케이스 개수가 주어지고 각 케이스에 학생의 수와 점수가 주어진다.    
각 케이스별로 평균을 구하고 그 평균을 넘는 학생 수를 구한 뒤, 비율로 나타내면 되므로 그리 어려운 문제는 아니었다.    


#### 1. StringBuilder, 형변환
```java
package Step6;

import java.io.*;
import java.util.StringTokenizer;

public class Step6_4344_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int sum = 0;
        int average = 0;
        int[] test_case;
        int cnt = 0;
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < n; i++) {
            sum = 0;
            cnt = 0;
            st = new StringTokenizer(br.readLine());
            int stNum = Integer.parseInt(st.nextToken());
            test_case = new int[stNum];

            for (int j = 0; j < stNum; j++) {
                test_case[j] = Integer.parseInt(st.nextToken());
                sum += test_case[j];
            }

            average = sum / stNum;

            for (int j = 0; j < stNum;j++) {
                if (test_case[j] > average) {
                    cnt++;
                }
            }

            sb.append(String.format("%.3f", ((double)cnt / stNum) * 100.0)).append("%\n");
        }

        System.out.print(sb);
    }
}
```    

변수를 int로 설정하고 나중에 (double)로 형변환을 한 뒤 계산하도록 했다. 평균과 학생들의 점수는 int로 받고 계산해도 
문제가 없으므로 int로 설정했으나 세자리수까지 계산하기위해 형변환을 했다.    


#### 2. BufferWriter, 형변환
```java
package Step6;

import java.io.*;
import java.util.StringTokenizer;

public class Step6_4344_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int n = Integer.parseInt(br.readLine());
        int sum = 0;
        int average = 0;
        int[] test_case;
        int cnt = 0;
        StringTokenizer st;

        for (int i = 0; i < n; i++) {
            sum = 0;
            cnt = 0;
            st = new StringTokenizer(br.readLine());
            int stNum = Integer.parseInt(st.nextToken());
            test_case = new int[stNum];

            for (int j = 0; j < stNum; j++) {
                test_case[j] = Integer.parseInt(st.nextToken());
                sum += test_case[j];
            }

            average = sum / stNum;

            for (int j = 0; j < stNum;j++) {
                if (test_case[j] > average) {
                    cnt++;
                }
            }

            bw.write(String.format("%.3f", ((double)cnt / stNum) * 100.0));
            bw.write("%\n");
        }
        br.close();
        bw.flush();
        bw.close();
    }
}
```    

작성은 같으나 buffer를 사용해 출력해봤다.     


#### 3. double 변수 설정
```java
package Step6;

import java.io.*;
import java.util.StringTokenizer;

public class Step6_4344_3 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        double sum = 0;
        double average = 0;
        int[] test_case;
        double cnt = 0;
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < n; i++) {
            sum = 0;
            cnt = 0;
            st = new StringTokenizer(br.readLine());
            int stNum = Integer.parseInt(st.nextToken());
            test_case = new int[stNum];

            for (int j = 0; j < stNum; j++) {
                test_case[j] = Integer.parseInt(st.nextToken());
                sum += test_case[j];
            }

            average = sum / stNum;

            for (int j = 0; j < stNum;j++) {
                if (test_case[j] > average) {
                    cnt++;
                }
            }

            sb.append(String.format("%.3f", (cnt / stNum) * 100.0)).append("%\n");
        }

        System.out.print(sb);
    }
}
```    

형변환을 하는 대신, 애초에 변수를 double로 입력받도록 해봤다. 형변환을 하는 것과 아닌 것 사이에 
어떤 차이가 있을지 궁금했다.    
    
    
![image](https://user-images.githubusercontent.com/68698007/133965093-e0f67eb8-c405-4d52-bf75-27248b7c0444.png)
1. 3번
2. 2번
3. 1번

