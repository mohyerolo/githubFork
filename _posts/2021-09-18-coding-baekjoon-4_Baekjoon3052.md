---
title: 백준 3052(나머지) - 1차원 배열
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/3052
### 수 10개를 입력받은 뒤, 이를 42로 나눈 나머지를 구한다. 그 다음 서로 다른 값이 몇 개 있는지 출력하는 프로그램을 작성하시오.
첫째 줄부터 열번째 줄 까지 숫자가 한 줄에 하나씩 주어진다. 이 숫자는 1,000보다 작거나 같고, 음이 아닌 정수이다.    
첫째 줄에, 42로 나누었을 때, 서로 다른 나머지가 몇 개 있는지 출력한다.    


42로 나눴을 때 나오는 수 중 다른 값의 개수를 세면 된다.    

### 1. 중첩 for문으로 비교
```java
package Step6;

import java.io.*;

public class Step6_3052_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int result = 0;
        int arr[] = new int[10];
        int i, j;

        for (i = 0; i < 10; i++) {
            arr[i] = Integer.parseInt(br.readLine()) % 42;
            for (j = 0; j < i; j++) {
                if (arr[j] == arr[i]) {
                    break;
                }
            }
            if (j == i) {
                result++;
            }
        }

        System.out.println(result);
    }
}    
```    
제일 먼저 생각났던 방법. 우선 배열 arr에 입력받은 수를 넣고 그 이전 값들중에서 
겹치는 게 있는지를 확인해본다. 있다면 벗어나서 j와 i의 값이 같지 않고 없다면 j가 i값까지 가므로 
j == i가 성립된다.    
이 방식은 for문 중첩이다보니 훨씬 시간이 오래걸릴것이다.    


### 2. boolean 배열로 확인
```java
package Step6;

import java.io.*;

public class Step6_3052_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        boolean[] arr = new boolean[42];
        
        for (int i = 0; i < 10; i++) {
            arr[Integer.parseInt(br.readLine()) % 42] = true;
        }

        int cnt = 0;
        for (boolean value : arr) {
            if (value) {
                cnt++;
            }
        }
        System.out.println(cnt);
    }
}    
```    

1번에서는 int배열로 각 수를 저장했다. 그러나 생각해보면 입력받는 수보다는 겹치는 게 있냐 없냐가 중요한 것이다.    
이는 boolean배열로 확인하면서 하는 게 훨씬 나은 방법이 된다는 것이다.    
10개의 입력받은 수를 42로 나눈 값을 arr배열의 각 인덱스로 넣어 true값으로 바꾼다.    

그 후, arr배열을 훑으며 true인 값이 있으면 cnt의 값을 증가시키고 이를 출력한다.    


### 3. HashSet
```java
package Step6;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.HashSet;

public class Step6_3052_3 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        HashSet<Integer> h = new HashSet<Integer>();
        
        for (int i = 0; i < 10; i++) {
            h.add(Integer.parseInt(br.readLine()) % 42);
        }

        System.out.print(h.size());
    }
}    
```     
대망의 HashSet. 이거를 보는 순간 분명 배웠는데 뭐지 싶어서 공부하다가 Collection 기본적인 걸 거의 다 공부했다.    
HashSet은 중복되지 않는 값만을 저장하므로 이걸 사용하면 어렵지 않게 이 풀이가 가능하다.    
HashSet.add()를 이용해 42로 나눈 수를 집합에 저장하고 집합의 사이즈를 출력하면 된다.    


![image](https://user-images.githubusercontent.com/68698007/133877450-2c944c22-0fff-48b5-83ea-14dc8b4d1983.png)
1. HashSet
2. boolean 배열
3. int 배열, 이중 for문
