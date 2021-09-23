---
title: 백준 2798(블랙잭) - 브루트 포스
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/2798>
### N장의 카드에 써져 있는 숫자가 주어졌을 때, M을 넘지 않으면서 M에 최대한 가까운 카드 3장의 합을 구해 출력하시오.
첫째 줄에 카드의 개수 N(3 ≤ N ≤ 100)과 M(10 ≤ M ≤ 300,000)이 주어진다. 둘째 줄에는 카드에 쓰여 있는 수가 주어지며, 이 값은 100,000을 넘지 않는 양의 정수이다.
합이 M을 넘지 않는 카드 3장을 찾을 수 있는 경우만 입력으로 주어진다.    
첫째 줄에 M을 넘지 않으면서 M에 최대한 가까운 카드 3장의 합을 출력한다.    

<hr>
3장의 합이 M에 최대한 가까운 수를 구해내는 문제이다. 

```java
package Step22;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step22_2798_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());
        
        int arr[] = new int[n];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        int result = search(arr, n, m);
        System.out.println(result);
    }

    public static int search(int[] arr, int n, int m) {
        int result = 0;
        for (int i = 0; i < n - 2; i++) {
            // 이미 첫 번째 카드가 m보다 크다면 넘기기
            if (arr[i] > m) continue;

            for (int j = i + 1; j < n - 1; j++) {
                if (arr[i] + arr[j] > m) continue;
                
                for (int k = j + 1; k < n; k++) {
                    int temp = arr[i] + arr[j] + arr[k];
                    if (temp == m) {
                        return temp;
                    }

                    if (temp < m && result < temp) {
                        result = temp;
                    }
                }
            }
        }

        return result;
    }

}
```
https://st-lab.tistory.com/97 이 분의 글을 봤다.    

첫 번째 for문과 두 번째 for문의 초기화값과 어디까지 반복해야되는지까지는 나도 생각할 수가 있었는데 확실히 그냥 내 생각으로는 마무리가 되지 않는 것 같다.    
<br>
코드를 자세히 살펴보겠다.    

첫 번째 for문의
```java
for (int i = 0; i < n - 2; i++) {
  if (arr[i] > m) continue;
  ...
}
```
이 부분에서 i < n - 2는 우리가 세 장을 살펴봐야되므로 맨 끝에서 세장전의 것까지만 보도록 하는 것이다. 그리고 이미 첫 번째 카드부터 주어진 최댓값을 넘는다면 
계속해서 합을 구할 의미가 없으므로 건너뛰도록 해준다.    

두 번째 for문에서는
```java
for (int j = i + 1; j < n - 1; j++) {
    if (arr[i] + arr[j] > m) continue;
    ...
}
```     
중복이 안 되니까 현재 i값보다 하나 앞의 값을 더해야되므로 i + 1로 초기화가 된다. 그리고 여기서부터는 이미 한 장이 뽑혔고 남은 두 장이게되므로 j가 n - 1의 값보다 
작을때 진행되어야한다. 그리고 여전히 이미 뽑은 카드와 현재 선택한 카드의 값이 최댓값을 넘긴다면 이번에 선택한 카드는 건너뛰도록 한다.    


세 번째 for문에서는
```java
for (int k = j + 1; k < n; k++) {
    int temp = arr[i] + arr[j] + arr[k];
    if (temp == m) {
        return temp;
    }

    if (temp < m && result < temp) {
        result = temp;
    }
}
```    

마지막 카드를 선택하는 것이다. 따라서 전에 뽑은 카드보다 한 칸 앞의 카드를 선택하니까 j + 1로 값이 잡힌다. 그리고 마지막 카드까지 선택이 가능하므로 k < n이 된다.    
이제 세 장의 합을 구한 후에 만약 합이 최댓값과 같다면 매우 적합한 숫자이므로 바로 return을 해준다. 그러나 그저 최댓값을 넘지 않고 이미 저장된 result값보다 크다면  
변수에 합을 저장하고 for문을 반복한다.     


세 개의 for문을 다 돈다면 모든 경우의 수를 다 짚어봤다는 것이므로 최댓값이 구해졌을 것이다. 그 값을 return해주면 된다.    

이런 문제에서는 모든 경우의 수를 다 살펴봐야되지만 어떤 경우에 그냥 넘어가도 되는지, 어떻게 보는 게 효율적인지를 잘 알아봐야 될 것 같다.
