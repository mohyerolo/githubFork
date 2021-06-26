---
title: 백준 10950(A + B - 3)
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/10950>
### 두 정수 A와 B를 입력받은 다음, A+B를 출력하는 프로그램을 작성하시오.    
첫째 줄에 테스트 케이스의 개수 T가 주어진다.    
각 테스트 케이스는 한 줄로 이루어져 있으며, 각 줄에 A와 B가 주어진다. (0 < A, B < 10)    
<hr>

백준 for단계 두 번째 문제로 두 수의 합을 구하는 문제다. 문제 자체는 어렵지 않고 앞에서 풀었던 문제들처럼
Scanner 또는 Buffer 사용으로 풀었다.    

#### 1. Scanner
이번에 스캐너는 두 번으로 나눠서 풀어봤다. 첫 번째는 입력과 동시에 출력을 하는 게 되는지 궁금해서
해봤는데 콘솔로 했을 때는 입력과 출력이 번갈아 나와서 문제이기는 했는데 백준에서는 문제없이 돌아갔다.    
1 - 1    
```java
import java.util.Scanner;

public class Step3_10950_1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int T = sc.nextInt();

        for (int i = 0; i < T; i++) {
            System.out.println(sc.nextInt() + sc.nextInt());
        }
        sc.close();
    }
}
```    
1 - 2
```java
import java.util.Scanner;

public class Step3_10950_2 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int T = sc.nextInt();

        int arr[] = new int[T];

        for (int i = 0; i < T; i++) {
            arr[i] = sc.nextInt() + sc.nextInt();
        }
        sc.close();

        for (int a : arr) {
            System.out.println(a);
        }
    }
}
```    

<br>

#### 2. BufferedReader, StringTokenizer    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step3_10950_3 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int T = Integer.parseInt(br.readLine());

        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < T; i++) {
            st = new StringTokenizer(br.readLine());
            sb.append(Integer.parseInt(st.nextToken()) + Integer.parseInt(st.nextToken()));
            sb.append('\n');
        }

        System.out.println(sb);
    } 
}
```    
StringTokenizer로 한 줄 씩 읽을때마다 띄어쓰기를 기준으로 분리시켜 StringBuilder로 저장했다.     


#### 3. BufferedReader, split    

```java
package Step3;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step3_10950_4 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int T = Integer.parseInt(br.readLine());

        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < T; i++) {
            String str = br.readLine();
            String[] arr = str.split(" ");
            sb.append(Integer.parseInt(arr[0]) + Integer.parseInt(arr[1])).append("\n");
        }

        System.out.println(sb);
    } 
}

```    
StringTokenizer대신 split으로 분리를 해서 배열에 저장된거를 더해봤다. 시간은 StringTokenizer를 사용한 것과 똑같았다.    

<br>
![image](https://user-images.githubusercontent.com/68698007/122888635-fe40d800-d37c-11eb-8dee-73b04e0de458.png)
1. Scanner, 배열 사용
2. BufferedReader, StringTokenizer
3. Scanner, 입력과 동시에 출력

