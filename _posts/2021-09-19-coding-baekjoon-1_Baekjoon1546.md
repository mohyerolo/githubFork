---
title: 백준 1546(평균) - 1차원 배열
layout: post
categories: coding
tags: baekjoon
---
### 세준이는 자기 점수 중에 최댓값을 골랐다. 이 값을 M이라고 한다. 그리고 나서 모든 점수를 점수 / M * 100으로 고쳤다. 예를 들어, 세준이의 최고점이 70이고, 수학점수가 50이었으면 수학점수는 50 / 70 * 100이 되어 71.43점이 된다. 세준이의 성적을 위의 방법대로 새로 계산했을 때, 새로운 평균을 구하는 프로그램을 작성하시오.

최댓값을 고르고 모든 점수를 최댓값 * 100으로 나누면 된다.    
소수점을 출력해야하므로 적어도 계산에 영향을 미칠 값 중 하나는 double이어야된다.    

#### 1. 배열, Arrays.sort()
```java
package Step6;

import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Step6_1546_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        double[] arr = new double[Integer.parseInt(br.readLine())];
        StringTokenizer st = new StringTokenizer(br.readLine());

        for (int i = 0; i < arr.length; i++) {
            arr[i] = Double.parseDouble(st.nextToken());
        }
        
        double sum = 0;
        Arrays.sort(arr);

        for (int i = 0; i < arr.length; i++) {
            sum += ((arr[i] / arr[arr.length - 1]) * 100);
        }
        System.out.println(sum / arr.length);
    }
}
```    

최댓값을 찾기 위해 Array.sort를 사용해 정렬하고 마지막 요소에 접근하는 방식을 사용했다. 입력 값을 double로 받아 저장하고 for문을 한 번 더 돌아 새로운 점수 값의 합을 더한다.    


#### 2. 배열 X
```java
package Step6;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step6_1546_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());

        StringTokenizer st = new StringTokenizer(br.readLine());

        int max = 0;
        double sum = 0;

        for (int i = 0; i < n; i++) {
            int score = Integer.parseInt(st.nextToken());
            if (max < score) {
                max = score;
            }
            sum += score;
        }

        System.out.println(((sum / max) * 100.0) / n);
    }
}
```    

입력과 동시에 max값을 알아내도록 한다. 그리고 입력 값을 전부 다 나누고 곱하는 방법보다는 어차피 과정에 필요한 값이 정해져 있으므로 
sum만 구하고 그 값을 /max * 100을 하면 되는 것이다. 그 후에 전체 개수로 나눠주면 더 쉽게 새로운 평균을 구할 수 있다.    


#### 3. 배열
```java
package Step6;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step6_1546_3 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        int n = Integer.parseInt(br.readLine());
        String[] scores = br.readLine().split(" ");
        int score;
        int sum = 0;
        int max = 0;
        for (int i = 0; i < scores.length; i++) {
            score = Integer.parseInt(scores[i]);
            sum += score;
            max = max < score ? score : max;
        }
        System.out.println((((double)sum / max) * 100.0) / n);
    }
}
```    

방법은 2와 비슷하나 배열을 사용한 방법이다. 여러가지 방법을 나 스스로 생각할 수 있도록 되고싶다... 이번에는 모두 int로 받고 계산할 때 
double로 형변환을 하는 방식으로 해봤다.    

![image](https://user-images.githubusercontent.com/68698007/133923084-31b9df4f-151b-4481-ae69-6523d38870f7.png)
![image](https://user-images.githubusercontent.com/68698007/133923090-0b67c7c2-5869-43ae-bdf1-363eab07a3d7.png)

1. 배열, Arrays.sort()
2. 배열
3. 배열 X
