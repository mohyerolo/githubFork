---
title: 백준 2580(스도쿠) - 백트래킹
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/2580>
### 게임 시작 전 스도쿠 판에 쓰여 있는 숫자들의 정보가 주어질 때 모든 빈 칸이 채워진 최종 모습을 출력하는 프로그램을 작성하시오.
아홉 줄에 걸쳐 한 줄에 9개씩 게임 시작 전 스도쿠판 각 줄에 쓰여 있는 숫자가 한 칸씩 띄워서 차례로 주어진다. 스도쿠 판의 빈 칸의 경우에는 0이 주어진다. 스도쿠 판을 규칙대로 채울 수 없는 경우의 입력은 주어지지 않는다.   

모든 빈 칸이 채워진 스도쿠 판의 최종 모습을 아홉 줄에 걸쳐 한 줄에 9개씩 한 칸씩 띄워서 출력한다.    
스도쿠 판을 채우는 방법이 여럿인 경우는 그 중 하나만을 출력한다.
<hr>
9x9에서 각 칸에 숫자가 써져있고 0으로 되어있는 곳을 수정해서 모든 숫자가 채워져 있도록 수정한 뒤에 출력하면 된다.    

스도쿠는 숫자가 있는 위치의 가로와 세로줄에 중복된 수가 없고 3 x 3으로 나눠진 박스 안에서도 겹치는 수가 없으면 되는 거다.    
즉, row와 col이 겹치지 않는지를 각각 검사하고, 0이 있는 곳의 3x3 박스의 위치(row, col)를 구한 뒤에 그 안에 포함되어 있는지를 보면 된다.    

이번 문제도 <https://st-lab.tistory.com/119?category=862595> 이 블로그를 보고 풀 수 있었다.    

<br>
9x9로 이루어진 스도쿠이므로 이차원 배열이 필요하고 각 입력을 BufferedReader로 받은 후 StringTokenizer로 분리해서 배열에 넣으면 된다. 그 후 arr[0][0]에서부터 확인해야하므로 dfs(0, 0)으로 이동한다.

```java
public class Step34_2580 {
    public static int[][] arr;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        arr = new int[9][9];

        for (int i = 0; i < 9; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 9; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        dfs(0, 0);
    }
}
```    

dfs에서는 종료를 위해 리턴문을 작성하고 0인 칸이 았을 경우 1부터 9까지 넣어보면서 확인할 수 있도록 만드는 거다.    
dfs로 넘어가는 매개변수를 각 행, 열로 뒀으므로 행과 열을 체크해서 리턴하면 된다.    
col이 9가 된다는 거는 배열 arr[]의 인덱스 0부터 8까지, 총 9칸을 다 체크해봤다는 얘기가 되므로 다음 줄로 이동하면 된다.    
row가 9라는 건 배열 arr의 모든 행을 다 살펴봤다는 것으로 여기까지 도달했다는 거는 모든 빈칸이 제대로 채워져 있다는 걸로 출력하면 된다.    

arr[row][col]이 0이면(빈칸) 1부터 9까지 반복문을 돌리며 어떤 수가 가능한지를 알아야한다. 만약 하나의 수가 가능하다는 걸 알게되면 arr[row][col]에 그 수를 넣고 다음 열로 이동하면 된다. 만약 그게 마지막 열이었으면 if문을 통해 다음 줄로 이동하는 것이다.    

그런데 arr[row][col]에 1부터 9까지 모든 수를 넣어봤는데 가능한 수가 하나도 없었다는 거는 이전 빈칸에 넣었던 수가 그때는 가능했어도 그 다음 빈칸을 채우려고보니 가능하지 않다는 걸 알게된 것으로 이전 빈칸을 다시 수정해야되는 경우가 된 것이다. 그러므로 arr[row][col]을 다시 0으로 수정하고 이전의 경우로 돌아가는 것이다. 그러면 전에 수정한 빈칸을 다시 수정하게된다.    

```java
public static void dfs(int row, int col) {
    // 한 줄이 다 체크되면 다음 줄로 이동
    if (col == 9) {
        dfs(row + 1, 0);
        return;
    }

    // 모든 줄이 다 체크됐으면 가능한 경우의 수가 생긴거므로 출력
    if (row == 9) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                sb.append(arr[i][j]).append(' ');
            }
            sb.append('\n');
        }
        System.out.println(sb);
        System.exit(0);
    }

    // 빈 칸이 있으면 1부터 9중에 가능한 수를 넣어야됨
    if (arr[row][col] == 0) {
        for (int i = 1; i <= 9; i++) {
            if (possibility(row, col, i)) {
                arr[row][col] = i;
                dfs(row, col + 1);
            }
        }
        /**
         * 만약 전에는 가능했던 수였는데 진행하다보니 그 후에 0으로 되어있던 칸들이
         * 맞지 않아서 나오게 되면 현재 진행했던 칸의 수는 다시 비워져서 이전으로 돌아가야됨.
         **/ 
        arr[row][col] = 0;
        return;
    }

    // arr[row][col]이 0이 아니면 다음 칸을 봐야됨
    dfs(row, col + 1);
}
```

그렇다면 arr[row][col]이 0일때 거기에 어떤 수가 가능한지를 알 수 있는 possibility 메소드를 작성해야한다. 이는 위에서 작성한대로 스도쿠의 규칙을 따르면 되는데 가로줄고 세로줄에 겹치는 수가 없고, 3x3으로 잘랐을 때 작은 박스 안에서도 겹치는 수가 없으면 된다.    

```java
public static boolean possibility(int row, int col, int n) {
    // 가로줄에 같은 수가 있는지 확인
    for (int i = 0; i < 9; i++) {
        if (arr[i][col] == n) return false;
    }

    // 세로줄에 같은 수가 있는지 확인
    for (int i = 0; i < 9; i++) {
        if (arr[row][i] == n) return false;
    }

    // 현재 9 x 9를 3 x 3으로 볼 때 어디에 위치하고 있는지를 확인
    int nRow = (row / 3) * 3;
    int nCol = (col / 3) * 3;

    // 3 x 3에서도 같은 수가 있는지 확인
    for (int i = nRow; i < nRow + 3; i++) {
        for (int j = nCol; j < nCol + 3; j++) {
            if (arr[i][j] == n) return false;
        }
    }

    // 가로, 세로줄, 작은 박스 안에서도 겹치는 수가 없다면 가능한 수인것.
    return true;
}
```

이렇게 코드가 완성된다.    

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Step34_2580 {
    public static int[][] arr;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        arr = new int[9][9];

        for (int i = 0; i < 9; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 9; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        dfs(0, 0);
    }

    public static void dfs(int row, int col) {
        // 한 줄이 다 체크되면 다음 줄로 이동
        if (col == 9) {
            dfs(row + 1, 0);
            return;
        }

        // 모든 줄이 다 체크됐으면 가능한 경우의 수가 생긴거므로 출력
        if (row == 9) {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < 9; i++) {
                for (int j = 0; j < 9; j++) {
                    sb.append(arr[i][j]).append(' ');
                }
                sb.append('\n');
            }
            System.out.println(sb);
            System.exit(0);
        }

        // 빈 칸이 있으면 1부터 9중에 가능한 수를 넣어야됨
        if (arr[row][col] == 0) {
            for (int i = 1; i <= 9; i++) {
                if (possibility(row, col, i)) {
                    arr[row][col] = i;
                    dfs(row, col + 1);
                }
            }
            /**
             * 만약 현재는 가능했던 수였는데 진행하다보니 그 후에 0으로 되어있던 칸들이
             * 맞지 않아서 나오게 되면 현재 진행했던 칸의 수는 다시 비워져서 이전으로 돌아가야됨.
             **/ 
            arr[row][col] = 0;
            return;
        }

        // arr[row][col]이 0이 아니면 다음 칸을 봐야됨
        dfs(row, col + 1);
    }

    public static boolean possibility(int row, int col, int n) {
        // 가로줄에 같은 수가 있는지 확인
        for (int i = 0; i < 9; i++) {
            if (arr[i][col] == n) return false;
        }

        // 세로줄에 같은 수가 있는지 확인
        for (int i = 0; i < 9; i++) {
            if (arr[row][i] == n) return false;
        }

        // 현재 9 x 9를 3 x 3으로 볼 때 어디에 위치하고 있는지를 확인
        int nRow = (row / 3) * 3;
        int nCol = (col / 3) * 3;

        // 3 x 3에서도 같은 수가 있는지 확인
        for (int i = nRow; i < nRow + 3; i++) {
            for (int j = nCol; j < nCol + 3; j++) {
                if (arr[i][j] == n) return false;
            }
        }

        // 가로, 세로줄, 작은 박스 안에서도 겹치는 수가 없다면 가능한 수인것.
        return true;
    }
}
```
