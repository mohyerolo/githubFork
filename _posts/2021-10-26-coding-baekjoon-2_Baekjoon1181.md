---
title: 백준 1181(단어 정렬) - 정렬
layout: post
categories: coding
tags: theory
---
<https://www.acmicpc.net/problem/1181>
### 알파벳 소문자로 이루어진 N개의 단어가 들어오면 길이가 짤은 것부터, 길이가 같으면 사전 순으로 정렬하는 프로그램을 작성하시오.
첫째 줄에 단어의 개수 N이 주어진다. (1 ≤ N ≤ 20,000) 둘째 줄부터 N개의 줄에 걸쳐 알파벳 소문자로 이루어진 단어가 한 줄에 하나씩 주어진다. 주어지는 문자열의 길이는 50을 넘지 않는다.    
조건에 따라 정렬하여 단어들을 출력한다. 단, 같은 단어가 여러 번 입력된 경우에는 한 번씩만 출력한다.    

<hr>
좌표 정렬에서 했듯이 여러 기준을 가지고 정렬하는 부분에서는 Comparator을 사용하면 된다.    
이번에는 Comparator를 명시적으로 작성한 것, 람다식 작성으로 나눠서 해봤다.    

#### 1. new Comparator
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.Comparator;

public class Step9_1181_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int N = Integer.parseInt(br.readLine());
        String[] str = new String[N];

        for (int i = 0; i < N; i++) {
            str[i] = br.readLine();
        }

        Arrays.sort(str, new Comparator<String>(){
            public int compare(String s1, String s2) {
                if (s1.length() == s2.length()) {
                    return s1.compareTo(s2);
                }
                else {
                    return s1.length() - s2.length();
                }
            }            
        });

        sb.append(str[0]).append('\n');
        for (int i = 1; i < N; i++) {
            if (!str[i].equals(str[i - 1])){
                sb.append(str[i]).append('\n');
            }
        }

        System.out.println(sb);
    }
}
```
Arrays.sort()부분에 comparator가 들어갈 부분을 익명으로 작성해 넣은 걸 볼 수 있다. 저렇게 넣는 것 말고 위에서 comparator 변수를 하나 만들어서 넣을 수도 있지만 그것보다는 저게 훨씬 깔끔한 것 같다.    

<br>

#### 2. 람다식
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;


public class Step9_1181_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int N = Integer.parseInt(br.readLine());
        String[] str = new String[N];

        for (int i = 0; i < N; i++) {
            str[i] = br.readLine();
        }

        Arrays.sort(str, (e1, e2) -> {
            if (e1.length() == e2.length()) {
                return e1.compareTo(e2);
            }
            else {
                return e1.length() - e2.length();
            }
        });

        sb.append(str[0]).append('\n');
        for (int i = 1; i < N; i++) {
            if (!str[i].equals(str[i - 1])){
                sb.append(str[i]).append('\n');
            }
        }

        System.out.println(sb);
    }
}
```
람다식으로 풀어봤다. Comparator생성 부분이 빠지니 훨씬 간결해보인다. 그렇지만 간결해보인다고 람다식을 남발했다가는 오히려 이해하기 힘들어질수도 있으니 적당히 사용하는 게 좋다고 한다.    

<br>

이렇게 두 번 풀어봤는데 수정하면서 똑같은 Arrays.sort()니까 시간 차가 없을 거라고 생각했는데 메모리, 시간이 둘 다 차이가 나서 놀랐다.    

<br>

![image](https://user-images.githubusercontent.com/68698007/138832919-7f137fe7-4879-4b82-97f2-e71f529f0b2d.png)

1. new Comparator
2. 람다식   
