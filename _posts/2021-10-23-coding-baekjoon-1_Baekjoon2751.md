---
title: 백준 2751(수 정렬 2) - 정렬
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/2751>
### N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.
첫째 줄에 수의 개수 N(1 ≤ N ≤ 1,000,000)이 주어진다. 둘째 줄부터 N개의 줄에는 수가 주어진다. 이 수는 절댓값이 1,000,000보다 작거나 같은 정수이다. 수는 중복되지 않는다.
<hr>

2750(수 정렬)과 달라진 점은 주어지는 수가 백만까지 가능하다는 것이다. 2750번에서는 1000까지였다. 자료의 개수가 확 커져서 1에서 풀었던 기본적인 정렬 방법들로는 해결이 되지 않을 수도 있다. 

1. Arrays.sort()
2. Selection Sort
3. Insertion Sort
4. Merge Sort
5. Quick Sort
6. Dual-Pivot Quick Sort
7. Counting Sort
8. Collections.sort()

이렇게 시도해봤는데 2,3번 정렬까지는 시간 초과가 뜨는 게 이해가 갔지만 merge랑 quick, dual-pivot까지도 시간초과가 뜨는 점에서 약간 놀랐다. 그래도 될 줄 알았는데.. Arrays.Sort는 dual-pivot을 사용할텐데 내가 작성했던 코드는 Insertion Sort없이 dual-pivot만 있는거여서 시간 초과가 뜨나보다.

Arrays.sort()는 달라진 점이 없으니 코드는 생략하겠다.    

<br>

7. Counting Sort
```java
import java.io.*;

public class Main {
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

자료가 절댓값 백만까지 가능하니 boolean으로 만드는 배열도 이백만개가 들어갈 수 있도록 잡는다.    
사실 백만개정도되면 Counting Sort도 안되지 않을까 싶었는데 이정도까지는 괜찮은가보다.    


8. Collections.sort()
```java
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(br.readLine());

        ArrayList<Integer> list = new ArrayList<>();
        for (int i= 0; i < n; i++) {
            list.add(Integer.parseInt(br.readLine()));
        }

        Collections.sort(list);

        for (int value : list) {
            sb.append(value).append('\n');
        }
        
        System.out.println(sb);
    }
}
```
Collection Sort는 TimSort를 사용한다. Arrays.sort()에서도 객체를 정렬할 때 사용한다고 했던 것처럼 Tim Sort는 삽입, 합병 정렬이 합쳐진 형태이다. 각자 최선의 경우인 O(n), O(nlogn)을 가지고 있으므로 Tim sort는 O(n)에서 O(nlogn)의 시간을 보장한다.    
그런데 Collection sort를 사용하려면 리스트의 형태로 만든다음 정렬해야된다는 부분이 있다.    


![image](https://user-images.githubusercontent.com/68698007/138545447-1bfdfc40-868e-4753-bd25-ff9374ba43fb.png)

1. Dual-Pivot Quick Sort
2. Quick Sort
3. Merge Sort
4. Insertion Sort
5. Selection Sort
6. Arrays.sort()
7. Counting Sort
8. Collections.sort()

