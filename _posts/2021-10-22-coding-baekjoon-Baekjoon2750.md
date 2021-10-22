---
title: 백준 2750(수 정렬) - 정렬
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/2750>
### N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.

첫째 줄에 수의 개수 N(1 ≤ N ≤ 1,000)이 주어진다. 둘째 줄부터 N개의 줄에는 수가 주어진다. 이 수는 절댓값이 1,000보다 작거나 같은 정수이다. 수는 중복되지 않는다.

<hr>
정렬에 관한 문제다. 정렬 파트를 풀기위해 주구장창 정렬 이론만 공부하다가 왔다. 

N개의 수가 주어지고 정렬하기만 하면 되므로 복잡한 과정은 필요없이 단순히 들어오는 수를 배열에 저장하고 정렬한다.    

<br>

1. Arrays.sort()
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

// Arrays.sort 사용
public class Step9_2750_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }

        Arrays.sort(arr);

        for (int i : arr) {
            sb.append(i).append('\n');
        }

        System.out.println(sb);
    }
}
```    
Arrays.sort()를 사용해봤다. 객체가 아닌 경우에는 dual-pivot quick sort를 사용하는 것으로 알고 있다. quick sort와 시간은 똑같지만 o(n<sup>2</sup>)이 나올 확률을 줄여주고 좀 더 효율적인 것으로 알고있다.    

<br>

2. Selection Sort
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

// Selection Sort 사용
public class Step9_2750_2 {
    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    private static void selectionSort(int[] arr, int n) {
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }
            swap(arr, minIndex, i);
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }

        selectionSort(arr, arr.length);

        for (int i : arr) {
            sb.append(i).append('\n');
        }

        System.out.println(sb);
    }
}
```    

제일 기본적인 정렬 중 하나인 선택 정렬을 사용해봤다. 배열에서 최솟값을 가진 인덱스를 골라 0번째부터 바꿔나가는 것으로 시간 초과나지 않을까 싶었는데 돌아가서 놀랐다.    
<br>

3. Insertion Sort
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

// Insertion Sort 사용
public class Step9_2750_3 {
    private static void insertionSort(int[] arr, int n) {
        for (int i = 1; i < n; i++) {
            int k = arr[i];
            int j = i - 1;
            while (j >= 0 && arr[j] > k) {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = k;
        }
    }
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }

        insertionSort(arr, arr.length);

        for (int i : arr) {
            sb.append(i).append('\n');
        }

        System.out.println(sb);
    }
}
```
2번처럼 기본적인 정렬인 삽입 정렬을 사용해봤다. 이것도 선택정렬과 비슷한 시간으로 돌아간다.    

<br>

4. Counting Sort
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

// Counting Sort 사용
public class Step9_2750_4 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());
        boolean[] arr = new boolean[2001];      // 절댓값이 1000보다 작거나 같다고 했으니까

        for (int i = 0; i < n; i++) {
            arr[Integer.parseInt(br.readLine()) + 1000] = true;
        }       

        for (int i = 0; i < arr.length; i++) {
            if (arr[i]) {
                sb.append(i - 1000).append('\n');
            }
        }
        System.out.println(sb);
    }
}
```
범위가 크지 않다면 숫자를 정렬할 때 가장 많이 쓰는 Counting Sort를 사용해봤다.
교과서적이게 배열을 두 개나 더 추가로 만드는 방법이 아닌 중복되는 수가 없으므로 boolean 배열로 수를 받아 그것만 사용해 카운팅정렬을 하는 것이다.    
배열의 값이 true라면 수가 있는것이므로 출력할 수 있게 StringBuilder로 저장하는 것이다.

<br>

![image](https://user-images.githubusercontent.com/68698007/138433120-65aa04a7-fcea-4eec-b4ea-8d9f8fa85810.png)
![image](https://user-images.githubusercontent.com/68698007/138433159-8b8cfe44-cd91-46ac-b848-8ebe16e8cab7.png)
![image](https://user-images.githubusercontent.com/68698007/138433195-2702fa20-2a33-43e4-893f-1747bcfb769b.png)
![image](https://user-images.githubusercontent.com/68698007/138433215-7ccaff99-dd1a-4148-a5ad-15ac905627d7.png)

1. Arrays.sort()
2. Selection Sort
3. Insertion Sort
4. Counting Sort
