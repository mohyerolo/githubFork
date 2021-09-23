---
title: 백준 1018(체스판 다시 칠하기) - 브루트 포스
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/1018>
###  M * N 크기의 보드를 8 * 8 크기의 체스판으로 만들려고 한다. 지민이가 다시 칠해야 하는 정사각형의 최소 개수를 구하는 프로그램을 작성하시오.
첫째 줄에 N과 M이 주어진다. N과 M은 8보다 크거나 같고, 50보다 작거나 같은 자연수이다. 둘째 줄부터 N개의 줄에는 보드의 각 행의 상태가 주어진다. B는 검은색이며, W는 흰색이다.
첫째 줄에 지민이가 다시 칠해야 하는 정사각형 개수의 최솟값을 출력한다.    
<hr>

가로와 세로가 주어질 때 8 * 8로 만들 수 있는 경우의 수를 따져야되고, 그 안에서 첫 시작이 흰색 또는 검은색일 경우에 제대로 색칠되지 않은 칸의 개수를 
알아내야한다.    

이 문제는 내가 스스로 생각해내지 못했다.    
<https://st-lab.tistory.com/101?category=855026> 이 분의 블로그를 보고 해결할수 있었다.    

```java
package Step22;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step22_1018_1 {
    public static boolean[][] arr;
    public static int min = 64; // 맨 처음 정해지는 거는 무조건 정상이지만 그 외의 것이 다 틀릴경우가 63임.

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        arr = new boolean[N][M];

        for (int i = 0; i < N; i++) {
            String str = br.readLine();

            for (int j = 0; j < M; j++) {
                if (str.charAt(j) == 'W') {
                    arr[i][j] = true;   // W일 때는 true
                }
                else {
                    arr[i][j] = false;  // B일 때는 false
                }
            }
        }

        int N_row = N - 7;      // 0번 인덱스부터 입력된 수에서 7만큼 뺀 인덱스까지 가야지만 8칸 확보가 가능하므로
        int M_col = M - 7;

        for (int i = 0; i < N_row; i++) {
            for (int j = 0; j < M_col; j++) {
                find(i, j);
            }
        }

        System.out.println(min);
    }

    public static void find(int x, int y) {
        int end_x = x + 8;
        int end_y = y + 8;
        int cnt = 0;

        boolean TF = arr[x][y];     // 첫 번째 칸의 색
        for (int i = x; i < end_x; i++) {
            for (int j = y; j < end_y; j++) {
                if (arr[i][j] != TF) {
                    cnt++;
                }
                // 다음 칸은 색이 바뀌므로 변경 필요
                TF = !TF;
            }
            // 한 줄이 바뀌면 전 줄의 마지막 색이 이번 줄의 처음이 되어야 함.
            TF = !TF;
        }

        /**
         * 첫 번째 칸을 기준으로 할 때의 색칠할 개수와
         * 첫 번째 칸의 색의 반대되는 색을 기준으로 할 때의
         * 색칠할 개수(64 - cnt) 중 최솟값을 저장
         */
        cnt = Math.min(cnt, 64 - cnt);

        /**
         * 이전까지의 경우 중 최솟값보다 현재 cnt값이 
         * 더 작을 경우 최솟값 갱신
         */
        min = Math.min(min, cnt);
    }
}
```

이걸 어떻게 생각해내시는지.. 너무 대단.... 이해는 했는데 이걸 생각해낸다는 것 자체가 신기하다.
