---
title: 백준 10814(나이순 정렬) - 정렬
layout: post
categories: coding
tags: theory
---
<https://www.acmicpc.net/problem/10814>
### 회원들을 나이가 증가하는 순으로, 나이가 같으면 먼저 가입한 사람이 앞에 오는 순서로 정렬하는 프로그램을 작성하시오.
첫째 줄에 온라인 저지 회원의 수 N이 주어진다. (1 ≤ N ≤ 100,000)

둘째 줄부터 N개의 줄에는 각 회원의 나이와 이름이 공백으로 구분되어 주어진다. 나이는 1보다 크거나 같으며, 200보다 작거나 같은 정수이고, 이름은 알파벳 대소문자로 이루어져 있고, 길이가 100보다 작거나 같은 문자열이다. 입력은 가입한 순서로 주어진다.    

첫째 줄부터 총 N개의 줄에 걸쳐 온라인 저지 회원을 나이 순, 나이가 같으면 가입한 순으로 한 줄에 한 명씩 나이와 이름을 공백으로 구분해 출력한다.    
<hr>

앞에서 푼 단어 정렬과 비슷하다.    

처음 내가 코딩했던 건 String 배열로 두 개의 값을 받아들여 첫번째 값을 Integer.parseInt로 변형하고 계산하는 방식이었다.    

<br>

그러다 블로그를 보니까 StringBuilder 배열로 받는 방식을 보고 따라해봤다. <https://st-lab.tistory.com/113>


<br>

#### 1. String 배열
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.Comparator;
import java.util.StringTokenizer;

public class Step9_10814_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());
        String[][] arr = new String[n][2];

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            arr[i][0] = st.nextToken();
            arr[i][1] = st.nextToken();
        }

        Arrays.sort(arr, new Comparator<String[]>(){
            @Override
            public int compare(String[] o1, String[] o2) {
                // TODO Auto-generated method stub
                return Integer.parseInt(o1[0]) - Integer.parseInt(o2[0]);
            }
        });

        for (int i = 0; i < n; i++) {
            sb.append(arr[i][0]).append(' ').append(arr[i][1]).append('\n');
        }
        
        System.out.println(sb);
        
    }
}
```
위와같은 방법일 제일 빠르게 생각할 수 있는 방법이지 않을까 싶다.    

<br>

#### 2. StringBuilder 배열
<https://st-lab.tistory.com/113>

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step9_10814_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());
        StringBuilder[] p = new StringBuilder[201];

        for (int i = 0; i < p.length; i++) {
            p[i] = new StringBuilder();
        }

        for (int i = 0; i < n; i++) {;
            st = new StringTokenizer(br.readLine());
            int age = Integer.parseInt(st.nextToken());
            String name = st.nextToken();

            p[age].append(age).append(' ').append(name).append('\n');
        }
        
        for (StringBuilder val : p) {
            sb.append(val);
        }
        System.out.println(sb);
        
    }
}
```    

StringBuilder 배열을 201로 두는 이유는 StringBuilder를 Counting sort처럼 사용하기 위해서다.    
age를 인덱스로 이용하면 Counting sort를 사용한 것 처럼 정렬할 수 있게된다.    
<br>

![image](https://user-images.githubusercontent.com/68698007/139044838-20a63818-b066-4c5a-8e08-81bdcd821a20.png)

1. StringBuilder 배열
2. String 배열
