---
title: 백준 2231(분해합) - 브루트 포스
layout: post
categories: coding
tags: baekjoon
---
<https://www.acmicpc.net/problem/2231>
### 자연수 N이 주어졌을 때, N의 가장 작은 생성자를 구해내는 프로그램을 작성하시오.
어떤 자연수 N이 있을 때, 그 자연수 N의 분해합은 N과 N을 이루는 각 자리수의 합을 의미한다. 
어떤 자연수 M의 분해합이 N인 경우, M을 N의 생성자라 한다. 
예를 들어, 245의 분해합은 256(=245+2+4+5)이 된다. 따라서 245는 256의 생성자가 된다. 
물론, 어떤 자연수의 경우에는 생성자가 없을 수도 있다. 반대로, 생성자가 여러 개인 자연수도 있을 수 있다.

첫째 줄에 답을 출력한다. 생성자가 없는 경우에는 0을 출력한다.    
<hr>
이 문제는 학교에서도 한 번 푼 적이 있는 것 같다. 문제 자체는 나에게 크게 어렵지 않았으나 i의 초기값을 정하는 게 어려웠다. 어느 지점부터 시작해야 
최소한의 반복으로 계산을 할 수 있을지를 알아야되는데 그게 어디서부터인지를 모르겠더라... 지금까지 알고리즘 풀면서 내가 수학에 진짜 약하다는 걸 알게 되는듯...    

#### 내가 생각한 풀이
```java
package Step22;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step22_2231_1 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int i;

        for (i = N / 2; i < N; i++) {
            int sum = i;
            int n = i;
            while (n > 0) {
                sum += (n % 10);
                n /= 10;
                if (sum > N) {
                    break;
                }
            }
            if (sum == N) {
                System.out.println(i);
                break;
            }
        }
        if (i == N) {
            System.out.println("0");
        }
    }
}
```    

for문에서 i의 초기값을 N / 2로 한 이유는 굳이 처음부터 다 할 필요가 없다는 건 알고있지만 어디부터 하는 게 좋을지 모르겠어서 임의로 설정한 것이다.    
적어도 주어진 값을 2로 나눈 것보다는 더 큰 수에서 시작해도 된다는 것은 알기 때문에 2로 나눈 것이다.    
그리고 혹시 sum값이 i값의 각 자리별로 더하는 과정에서 커진다면 나가도 된다고 해놓은 것인데 생각해보니 작을 수는 있어도 클 수는 없는 것 같네.. 아닌가...    


<hr>
맞기는 했는데 잘 모르겠어서 블로그를 찾아봤다.    

#### <https://st-lab.tistory.com/98?category=855026> 
여기를 매번 보게되는듯.    

이 블로그를 보면 입력된 정수의 자릿수만큼 9를 곱한다음 빼면 된다고 설명한다.     
N은 생성자 + 생성자의 각 자릿수의 합인것이다. 즉 생성자 = N - 생성자의 각 자릿수의 합이 된다.    
그런데 각 자릿수는 9가 최대이다. 그러면 9를 자릿수의 길이만큼 곱한 값이 각 자릿수의 최대 합이 된다.    

즉, N - (9 * 생성자 자릿수 길이) 미만의 값은 생성자가 될 수 없다. 그러므로 거기서부터 탐색을 시작하면 된다.    

```java
package Step22;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Step22_2231_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();
        int N = Integer.parseInt(str);
        int i;

        for (i = (N - (str.length() * 9)); i < N; i++) {
            int sum = i;
            int n = i;
            while (n > 0) {
                sum += (n % 10);
                n /= 10;
            }
            if (sum == N) {
                System.out.println(i);
                break;
            }
        }
        if (i == N) {
            System.out.println("0");
        }
    }
}
```    

그래서 여기서 N을 문자로 받아 길이를 알아내고 거기서부터 탐색을 시작하도록 하는 것이다.    


![image](https://user-images.githubusercontent.com/68698007/134501826-9dccabe0-847b-48ff-aed5-d4a0d5c7a818.png)
1. N - (9 * str.length)
2. N / 2

<br>
이렇게 머리를 굴려서 알아내는 거에 익숙해지고 스스로 생각할 수 있으려면 많은 노력이 필요하겠다는 걸 더 깨닫게 됐다..
