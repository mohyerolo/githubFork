---
title: Radix Sort
layout: post
categories: coding
tags: theory
---

## Radix Sort
기수 정렬은 입력이 모두 k 자릿수 이하의 자연수인 특수한 경우에 (제한된 종류인 알파벳도 해당) 사용할 수 있는 방법으로 Θ(n) 시간이 소요되는 정렬 알고리즘이다.    

낮은 자릿수부터 비교하여 정렬해가는 것으로, 우선 가장 낮은 자릿수만 가지고 모든 수를 정렬한다. 그 다음 가장 낮은 자릿수는 잊어버린다. 앞과 같은 방법으로 더 이상 자릿수가 남지 않을 때까지 계속하면 마지막에는 정렬된 배열을 갖게된다.    


자릿수로 비교하며 정렬하기위해 테이블만큼의 공간이 추가로 필요하다. 이 공간에 각 자릿수의 값을 차례대로 넣어주는 방법을 k번 반복하는데 k가 상수이므로 전체 시간은 O(n)이 된다.     

자릿수를 차례로 정렬해나가는 작업에서 한자리씩 정렬을 하게되니까 counting Sort의 방법이 사용된다.    

```java
public class RadixSort {
    private static void digitSort(int[] arr, int digit) {
        int[] bucket = new int[arr.length];
        int[] count = new int[10];

        for (int i = 0; i < arr.length; i++) {
            count[(arr[i] / digit)% 10]++; 
        }

        for (int i = 1; i < count.length; i++) {
            count[i] += count[i - 1];
        }

        for (int i = arr.length - 1; i >= 0; i--) {
            bucket[--count[(arr[i] / digit) % 10]] = arr[i];
        }

        for (int i = 0; i < arr.length; i++) {
            arr[i] = bucket[i];
        }
    }

    private static int getMax(int[] arr) {
        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (max < arr[i]) {
                max = arr[i];
            }
        }
        return max;
    }

    private static void radixSort(int[] arr) {
        // 최댓값의 자릿수가 가장 클 것
        int max = getMax(arr);
        
        for (int i = 1; max / i > 0; i *= 10) {
            digitSort(arr, i);
        }
    }

    public static void main(String[] args) throws Exception {
        int[] arr = { 123, 2154, 222, 4, 283, 1560, 1061, 2150};
        radixSort(arr);

        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

알고리즘자체는 Counting Sort를 이해하고 난 후면 어렵지 않다.    
O(n)의 시간이 드는 각업을 자릿수만큼 하므로 시간 복잡도는 O(k(n))이 된다. 

기수 정렬이 그렇게 많이 사용되지 않은 이유는 매우 큰 숫자 또는 32비트 및 64비트 숫자와 같은 다른 값을 취하면 선형 시간에 수행할 수는 있지만 중간에 정렬하는데 너무 많은 공간을 차지하기 때문이다.    

