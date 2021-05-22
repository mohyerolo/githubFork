---
title: 백준2751(수정렬2)
categories: coding
tags: baekjoon
comments: true
layout: post
---
<https://www.acmicpc.net/problem/2751>
#### N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.
수 정렬1때 썼던 Arrays.sort()를 썼더니 시간이 너무 오래걸렸다
```java
public class Step12_2751 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());

        int[] arr = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }

        Arrays.sort(arr);
        
        for (int num : arr) {
            sb.append(num).append("\n");
        }
        System.out.println(sb);

        br.close();
    }
}
```

<https://st-lab.tistory.com/106?category=857114>
Collection을 사용하는 방법


수 정렬1때 사용해본 Counting Sort도 사용해봄
```java
public class Step12_2751 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());

        boolean[] arr = new boolean[2000001];

        for (int i = 0; i < n; i++) {
            arr[Integer.parseInt(br.readLine()) + 1000000] = true;
        }

        for (int i = 0; i < arr.length; i++) {
            if (arr[i]) {
                sb.append(i - 1000000).append('\n');
            }
        }

        System.out.println(sb);
        br.close();
    }
}
```

![image](https://user-images.githubusercontent.com/68698007/111025630-b5e25780-8428-11eb-94f6-fe14e75de0f0.png)
세번째로 해 본 계수 정렬이 역시나 제일 빠른것을 확인할 수 있다.
