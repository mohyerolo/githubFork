---
title: 백준 11650(좌표 정렬하기) - 정렬
layout: post
categories: coding
tags: theory
---
<https://www.acmicpc.net/problem/11650>
### 2차원 평면 위의 점 N개가 주어진다. 좌표를 x좌표가 증가하는 순으로, x좌표가 같으면 y좌표가 증가하는 순서로 정렬한 다음 출력하는 프로그램을 작성하시오.
첫째 줄에 점의 개수 N (1 ≤ N ≤ 100,000)이 주어진다. 둘째 줄부터 N개의 줄에는 i번점의 위치 x<sub>i</sub>와 y<sub>i</sub>가 주어진다. (-100,000 ≤ x<sub>i</sub>, y<sub>i</sub> ≤ 100,000) 좌표는 항상 정수이고, 위치가 같은 두 점은 없다.    

<hr>
Comparator와 Comparable을 공부한 이유가 여기있다.    

x, y좌표가 주어지고 기준이 하나가 아닌 두 개로 나눠지므로 Comparator을 사용해서 정렬을 하면 된다.    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Step9_11650_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();

        int N = Integer.parseInt(br.readLine());
        int[][] arr = new int[N][2];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            arr[i][0] = Integer.parseInt(st.nextToken());
            arr[i][1] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(arr, (e1, e2) -> {
            if (e1[0] == e2[0]) {
                return e1[1] - e2[1];
            }
            else {
                return e1[0] - e2[0];
            }
        });

        for (int i = 0; i < N; i++) {
            sb.append(arr[i][0]).append(" ").append(arr[i][1]).append('\n');
        }
        System.out.println(sb);
    }
}
```
여기서 Comparator를 어디서 쓰고 있냐 하면 Arrays.sort()부분이다. 저번에 작성했듯이 Arrays.sort()와 Collections.sort()에서는 두번째 매개변수에 Comparator가 들어갈 수 있다. 그런데 new Comparator부분이 없이 (e1, e2)가 있는 게 어떻게 같냐면 이는 람다식이다.    

<br>

람다식, 람다 함수는 익명 함수를 지칭하는 용어로 주로 함수에 인자로 전달되거나 돌려주는 결과값으로 쓰인다.     

여기서는 e1, e2가 매개변수로 들어가고, e1[0]과 e2[0](x 좌표의 값)의 값이 같으면 y좌표를 비교해 y좌표를 기준으로 오름차순 정렬이 되도록 하는 것이고 x좌표의 값이 다르다면 x좌표를 기준으로 오름차순 정렬을 하겠다는 것이다. 즉 Comparator의 compare부분을 직접적으로 명시하지 않고 람다식으로 작성한 것이다.    

그 후는 배열 arr을 순차적으로 StringBuilder에 저장시켜 출력하는 것이다.    

포스팅했던 Comparator를 알고있으면 꽤 쉽게 풀 수 있을 것 같다.     
