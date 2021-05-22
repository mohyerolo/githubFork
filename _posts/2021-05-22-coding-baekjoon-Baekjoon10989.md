---
layout: post
title: 백준10989(수정렬3)
categories: coding
tags: baekjoon
comments: true
---
<https://www.acmicpc.net/submit/10989>
#### N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.
<hr>
시간 3초 제한, 메모리 512MB 제한으로 꽤 제한이 있는 문제였다<br>
카운팅 정렬 사용이지만 중복이 있으므로 int형으로 해야된다는 생각에 완전 이론 그대로 만든 걸 처음에 시도했더니
시간 초과가 났고 하면서도 날 것 같더라..<br>

* 처음 시도해본 코드
```java
public class Step12_10989 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());
        int num;
        int index;

        int[] arr = new int[n];
        int[] counting = new int[10001];
        int[] sort = new int[n];

        for (int i = 0; i < n; i++) {
            num = Integer.parseInt(br.readLine());
            arr[i] = num;
            counting[num]++;
        }

        for (int i = 1; i < counting.length; i++) {
            counting[i] = counting[i - 1] + counting[i];
        }

        for (int i = 0; i < n; i++) {
            index = counting[arr[n - i - 1]] - 1;
            counting[arr[n - i - 1]]--;
            sort[index] = arr[n - i  -1];
        }

        for (int value : sort) {
            System.out.println(value);
        }
    }
}
```

* 좀 더 생각해보다가 블로그 참고한 코드
```java
public class Step12_10989 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());
        int[] counting = new int[10001];

        for (int i = 0; i < n; i++) {
            counting[Integer.parseInt(br.readLine())]++;
        }

        for (int i = 1; i < counting.length; i++) {
            while (counting[i] > 0) {
                sb.append(i).append('\n');
                counting[i]--;
            }
        }

        System.out.println(sb);
    }
}
```
while부분에서 아 그렇네 했는데 생각해보면 당연했다. 이미 정렬된 상태로 있는거였으니까..
![image](https://user-images.githubusercontent.com/68698007/111026949-94856980-8430-11eb-922c-1c2e4dd07ea0.png)
