---
title: 백준 2753(윤년)
layout: post
categories: coding
tags: baekjoon
comments: true
---
<https://www.acmicpc.net/problem/2753>
### 연도가 주어졌을 때, 윤년이면 1, 아니면 0을 출력하는 프로그램을 작성하시오.
윤년은 연도가 4의 배수이면서, 100의 배수가 아닐 때 또는 400의 배수일 때이다.    
예를 들어, 2012년은 4의 배수이면서 100의 배수가 아니라서 윤년이다. 1900년은 100의 배수이고 400의 배수는 아니기 때문에 윤년이 아니다. 하지만, 2000년은 400의 배수이기 때문에 윤년이다.    
<hr>

이번에도 두 가지 방식으로 풀어보기로 했다.
#### 1. Scanner
```java
package Step4;

import java.util.Scanner;

public class Step4_2753_1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int year = sc.nextInt();
        /*if (year % 4 == 0 && (year % 100 != 0 || year % 400 == 0)) {
            System.out.println("1");
        }
        else {
            System.out.println("0");
        }*/

        System.out.println((year % 4 == 0 && (year % 100 != 0 || year % 400 == 0)) ? 1 : 0);
        sc.close();
    }
}
```

- if-else 사용
![image](https://user-images.githubusercontent.com/68698007/121769260-8b29ab80-cb9d-11eb-9a15-4c7eb073447a.png)
<br>    
- 삼항연산자 사용
![image](https://user-images.githubusercontent.com/68698007/121769288-b2807880-cb9d-11eb-9bce-98475a178e44.png)
    
두 개도 약간의 차이는 있는데 미세하다.    

<br>

#### 2. BufferedReader

```java
package Step4;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step4_2753_2 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        int year = Integer.parseInt(br.readLine());
        System.out.println((year % 4 == 0 && (year % 100 != 0 || year % 400 == 0)) ? 1 : 0);
    }
}
```    
하나의 값만 받으므로 Buffer를 써야하나 싶었지만 막상 사용하고 실행결과를 보니 그래도 BufferedReader가 Scanner보다는 성능이 좋다는 걸 확인한 기분    
![image](https://user-images.githubusercontent.com/68698007/121769348-1c991d80-cb9e-11eb-9fe8-a0156aa4b90a.png)
    
