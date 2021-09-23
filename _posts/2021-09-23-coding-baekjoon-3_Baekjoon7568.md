---
title: 백준 7568(덩치) - 브루트 포스
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/7568>
### 학생 N명의 몸무게와 키가 담긴 입력을 읽어서 각 사람의 덩치 등수를 계산하여 출력해야 한다.
두 사람 A 와 B의 덩치가 각각 (x, y), (p, q)라고 할 때 x > p 그리고 y > q 이라면 우리는 A의 덩치가 B의 덩치보다 "더 크다"고 말한다. 
예를 들어 어떤 A, B 두 사람의 덩치가 각각 (56, 177), (45, 165) 라고 한다면 A의 덩치가 B보다 큰 셈이 된다. 
그런데 서로 다른 덩치끼리 크기를 정할 수 없는 경우도 있다. 
예를 들어 두 사람 C와 D의 덩치가 각각 (45, 181), (55, 173)이라면 몸무게는 D가 C보다 더 무겁고, 키는 C가 더 크므로, "덩치"로만 볼 때 C와 D는 누구도 상대방보다 더 크다고 말할 수 없다.

N명의 집단에서 각 사람의 덩치 등수는 자신보다 더 "큰 덩치"의 사람의 수로 정해진다. 
만일 자신보다 더 큰 덩치의 사람이 k명이라면 그 사람의 덩치 등수는 k+1이 된다. 이렇게 등수를 결정하면 같은 덩치 등수를 가진 사람은 여러 명도 가능하다. 

첫 줄에는 전체 사람의 수 N이 주어진다. 
그리고 이어지는 N개의 줄에는 각 사람의 몸무게와 키를 나타내는 양의 정수 x와 y가 하나의 공백을 두고 각각 나타난다.<br>
입력에 나열된 사람의 덩치 등수를 구해서 그 순서대로 첫 줄에 출력해야 한다. 단, 각 덩치 등수는 공백문자로 분리되어야 한다.
<hr>
키와 몸무게, 둘 다 비교해봤을 때 두 개가 다 크다면 랭크가 올라가지만 하나라도 작으면 그 사람보다 큰 게 아닌 걸로 처리된다. 하나의 등수에 여러 명이 있을 수도 있다.    


한 사람이 키, 몸무게의 값을 갖고, 그 값들을 기억해야하므로 배열이 필요하다.    

```java
package Step22;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step22_7568_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();

        int[][] arr = new int[N][2];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            arr[i][0] = Integer.parseInt(st.nextToken());
            arr[i][1] = Integer.parseInt(st.nextToken());
        }

        for (int i = 0; i < N; i++) {
            int score = 1;
            for (int j = 0; j < N; j++) {
                if (i == j) continue; // 자기 자신과는 비교 X
                if (arr[i][0] < arr[j][0] && arr[i][1] < arr[j][1]) {
                    score++;
                }
            }

            sb.append(score).append(" ");
        }

        System.out.println(sb);
    }
}
```
두 개의 정보를 담아야되니까 2차 배열로 설정한다.    
처음 저장된 것부터 끝까지 살펴봐야되고 비교를 해야되므로 한 사람을 다른 사람 전부와 비교해야한다. 그래서 두 개의 for문이 0부터 시작한다.     
등수는 중복될 수 있으므로 하나의 등수에 저장된 사람이 있는지를 몰라도 된다. 그러므로 그냥 score를 하나씩 더해주면 된다.
