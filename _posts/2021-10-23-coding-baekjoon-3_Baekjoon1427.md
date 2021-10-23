---
title: 백준 1427(소트인사이드) - 정렬
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/1427>
### 수가 주어지면, 그 수의 각 자릿수를 내림차순으로 정렬해보자.
첫째 줄에 정렬하려고 하는 수 N이 주어진다. N은 1,000,000,000보다 작거나 같은 자연수이다.    
첫째 줄에 자릿수를 내림차순으로 정렬한 수를 출력한다.    
<hr>

오름차순이 아닌 내림차순이고 자릿수별로 정렬해야한다.    

#### 1. String으로 받고 charAt로 구분
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step9_1427_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        String str = br.readLine();
        int[] arr = new int[10];

        for (int i = 0; i < str.length(); i++) {
            arr[str.charAt(i) - '0']++;
        }

        for (int i = arr.length - 1; i >= 0; i--) {
            while (arr[i] > 0) {
                sb.append(i);
                arr[i]--;
            }
        }

        System.out.println(sb);
        
    }
}
```
처음 생각해낸 방법은 자릿수별로 나누는 것이므로 String으로 받은 다음에 charAt()로 각 자릿수를 Counting Sort와 같은 방법으로 arr 배열에 넣는 것이었다.    
그 후에 arr배열의 끝에서부터 0이상이라면 (해당하는 수가 있는 것) StringBuilder에 저장하고 출력하는 것이다.     

그런데 이 방법은 String으로 받으니까 그냥 int로 받고 할 수 있는 방법이 없나 했다가 찾은 방법이 2번이다.    

<br>

#### 2. int로 받고 연산을 통해 배열에 저장
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step9_1427_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[10];

        while (n > 0) {
            arr[n % 10]++;
            n /= 10;
        }

        for (int i = arr.length - 1; i >= 0; i--) {
            while (arr[i]-- > 0) {
                sb.append(i);
            }
        }

        System.out.println(sb);
        
    }
}
```
int로 받은 후, 수를 0이 되기전까지 10으로 나눠서 나머지를 배열의 인덱스로 넣는 것이다. 이렇게 하면 각 자릿수별로 배열에 저장이 가능하다.    

나는 이렇게 하는 게 좀 더 빠를 거라고 생각했는데 막상 제출해보니 시간 차이는 별로 없더라.    


<br>

![image](https://user-images.githubusercontent.com/68698007/138548957-700197e3-3ba2-43ea-94b0-af90a4940ea3.png)

1. 2번 방법
2. 1번 방법
<br>

메모리에서는 int형이 아껴지는 게 보이지만 시간은 오히려 int가 조금이라도 더 들었다는 거에서 연산하는 게 charAt로 뽑아내는 것보다 오래 걸린다는 것 같다.    

