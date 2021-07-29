---
title: 백준 10952(A + B - 5) - while
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/10952>
### 두 정수 A와 B를 입력받은 다음, A+B를 출력하는 프로그램을 작성하시오.
입력은 여러 개의 테스트 케이스로 이루어져 있다.
각 테스트 케이스는 한 줄로 이루어져 있으며, 각 줄에 A와 B가 주어진다. (0 < A, B < 10)
입력의 마지막에는 0 두 개가 들어온다.
<hr>    

백준에서 while 단계에 있는 문제로 나는 do-while문, while문을 이용해서 풀어봤다.    

#### 1. do-while
```java
package Step2;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step2_10952_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();

        int A = 0;
        int B = 0;

        do {
            st = new StringTokenizer(br.readLine());
            A = Integer.parseInt(st.nextToken());
            B = Integer.parseInt(st.nextToken());

            if (A != 0 && B != 0) {
                sb.append(A + B).append("\n");
            }
        } while(A != 0 && B != 0);
        
        System.out.println(sb);
        br.close();
    }
}
```    
입력의 마지막을 0 0으로 판단하므로 적어도 한 번은 돌아야 된다는 것이다. 그래서 do while문을 이용해봤다.
입력과 출력은 지금까지 했던 A + B문제와 다르지 않으므로 똑같지만 while문이 끝나게 되는 종료지점을 
A와 B가 둘다 0일경우로 지정해줬다.   

#### 2. while (StringTokenizer 사용)
```java
package Step2;
import java.io.*;
import java.util.StringTokenizer;

public class Step2_10952_2 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();

        int A = 0;
        int B = 0;
        st = new StringTokenizer(br.readLine());
        while ((A = Integer.parseInt(st.nextToken())) != 0 && (B = Integer.parseInt(st.nextToken())) != 0) {
            sb.append(A + B).append("\n");
            st = new StringTokenizer(br.readLine());
        }

        System.out.println(sb);
        br.close();
    }
}
```    

두 번째로는 StringTokenizer를 이용해 띄어쓰기를 기준으로 문자열을 구분해주는 방법을 이용했다.
while을 돌 때 검사하도록 조건안에 A와 B 값을 알도록 했다.    

#### 3. while (charAt 사용)
```java
package Step2;

import java.io.*;

public class Step2_10952_3 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int A = 0;
        int B = 0;
        String str = br.readLine();
        while ((A = str.charAt(0) - '0') != 0 && (B = str.charAt(2) - '0') != 0) {
            sb.append(A + B).append("\n");
            str = br.readLine();
        }
        
        System.out.println(sb);
        br.close();
    }
}
```    

StringTokenizer를 사용하는 대신 charAt를 이용해봤다.

<br>
![image](https://user-images.githubusercontent.com/68698007/127433055-fee476b4-6b4d-40b9-b679-877679fd52a8.png)

1. while (charAt)
2. while (StringTokenizer)
3. do-while
    
    
do-while가 while문은 검사 시기만 다를 뿐이다. 그러나 while문은 루프 내부에서 조건식의 진위 여부를 변경해야 해서 반복 횟수가 가변적이라고 할 수 ㅣㅆ따.
따라서 while문은 사용자의 입력이나 네트워크의 변화, 특정 신호의 입력 등 언제 발생할지 모르는 조건에 대해 반복할 때 쓰는 것이 적합하다.    
사용자의 입력이 무조건 한 번은 있어야 될 경우에는 do-while이 적합하다고 할 수 있다.
