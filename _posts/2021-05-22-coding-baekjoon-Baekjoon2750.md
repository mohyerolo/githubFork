---
title: 백준 2750(수 정렬)+Counting Sort
categories: coding
tags: baekjoon
comments: true
layout: post
---
<https://www.acmicpc.net/problem/2750>
#### N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.
<hr>
자바를 아직 잘 모르는 상태라 Arrays.sort()를 검색해보고 알게됐다<br>   
알고있는 여러 가지 정렬도 아직 제대로 사용하지 못 하고 있는 상태지만 가장 간단한 방법이 있으니 우선 Arrays.sort()를 사용해봄


```java
import java.io.*;
import java.util.Arrays;

public class Step12_2750 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
       
        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }
        
        Arrays.sort(arr);

        for (int num : arr) {
            System.out.println(num);
        }
    }
}
```
![image](https://user-images.githubusercontent.com/68698007/111023373-10c18200-841c-11eb-8200-9704164dce38.png)

 
<https://st-lab.tistory.com/105?category=857114>

* Counting Sort 발견
  * 시간복잡도: O(n) (퀵 정렬보다 훨씬 빠름)<br>
 1. 숫자가 몇 번 등장하는지 세어준다 -> 여기서 만약 갑자기 너무 큰 수가 나온다면 무의미한 순회가 발생할 수 있음.<br>
 2. 등장 횟수를 누적합으로 바꿔줌<br>
 3. 배열을 하나 더 만들어 원배열을 뒤에서부터 순회하며 누적합이 알려주는 위치에 따라 숫자를 집어넣음<br>
 4. 집어넣은 숫자의 누적합 -1씩 해주며 반복<br>
  * 두 수를 비교하는 과정이 없기 때문에 빠른 배치가 가능
  * counting 배열 선언이 필요: 10개의 원소 정렬하고자 하는데 수의 범위가 0~1억이라면 메모리 낭비가 매우 큼    
  즉, Counting Sort가 효율적이려면 수열의 길이보다 수의 범위가 극단적으로 크면 안 됨. 그래서 퀵 정렬이나 병합정렬이 선호되는 됨
  ```java
  public class Step12_2750 {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());
        
        // range: -1000 ~ 1000 절댓값이 1000보다 작거나 같기때문
        boolean[] arr = new boolean[2001];
    
        for (int i = 0; i < n; i++) {
            // -1000이면 인덱스가 0이 돼야하므로 +1000을 하는 것
            // 숫자가 존재하면 해당하는 boolean배열에 true로 표시
            arr[Integer.parseint(br.readLine()) + 1000] = true;
        }

        for (int i = 0; i < 2001; i++) {
            if (arr[i]) {
                sb.append(i - 1000).append('\n');
            }
        }

        System.out.println(sb);
    }
}
```
