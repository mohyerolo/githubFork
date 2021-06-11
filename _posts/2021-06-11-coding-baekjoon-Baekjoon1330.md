---
title: 백준 1330(두 수 비교하기)
categories: coding
tags: baekjoon
comments: true
layout: post
---
<https://www.acmicpc.net/problem/1330>
#### 두 정수 A와 B가 주어졌을 때, A와 B를 비교하는 프로그램을 작성하시오.
<hr>
if문 단계에 해당하는 1330문제는 예전에 풀었지만 처음부터 확실히 이해하고 싶은 마음에 다시 풀기 시작했다.
     
근데 예전에 Scanner만 알던 때와는 다르게 이렇게 간단한 문제여도 Buffer를 사용할수도 있다는 게 생각나서 약간 기분이 좋게 시작했다.    

1. Scanner    

```java
package Step4;
import java.util.Scanner;

public class Step4_1330_1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int A = sc.nextInt();
        int B = sc.nextInt();

        /*if (A > B) {
            System.out.println(">");
        }
        else if (A < B) {
            System.out.println("<");
        }
        else {
            System.out.println("==");
        }*/

        System.out.println((A == B) ? "==" : ((A < B) ? "<" : ">"));
        sc.close();
    }
}
```    
if - else만을 이용한 풀이와 삼항연산자를 이용한 풀이이다.
   
- 삼항연산자: (조건문) ? true일때의 값 : false일때의 값;
    
알고는 있었는데 중첩으로 만들 수 있다는 걸 이번에 블로그를 보면서 알게됐다.    

![image](https://user-images.githubusercontent.com/68698007/121683892-f4a3ae80-caf8-11eb-8567-a2779a89a728.png)    
    
2. Buffer    

버퍼로 입력된 수를 받아오는 방법으로 StringTokenizer를 이용해 띄어쓰기를 구분할 것이다.

```java
package Step4;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step4_1330_2 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        int A = Integer.parseInt(st.nextToken());
        int B = Integer.parseInt(st.nextToken());

        System.out.println((A == B) ? "==" : ((A < B) ? "<" : ">"));
    }
}

```    
![image](https://user-images.githubusercontent.com/68698007/121683960-08e7ab80-caf9-11eb-9078-7c77ecdd8510.png)

이렇게 하니 확실하게 메모리와 시간이 줄어든걸 알 수 있었다.
