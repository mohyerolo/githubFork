---
title: 병합 정렬(Merge Sort)
layout: post
categories: coding
tags: theory
---
기본적인 정렬 알고리즘은 모두 평균 Θ(n<sup>2</sup>)의 시간이 소요된다. 앞으로 포스팅할 정렬 알고리즘은 모두 평균 
Θ(nlogn)의 시간이 소요된다.    

병합 정렬의 경우 최악의 경우에도 O(nlogn)이 소요된다.    

## 병합 정렬(Merge Sort)
1. 리스트를 두 개의 균등한 크기로 분할하고 분할된 부분리스트를 정렬
2. 정렬된 두 개의 부분리스트를 합하여 전체 리스트 정렬

병합 정렬의 정렬 과정은 위와 같다. 이런 방법을 분할 정복(divide and conquer)방법이라고 한다.    
<br>

![image](https://user-images.githubusercontent.com/68698007/135703290-2df29f14-78fc-458b-9616-b5f3ad9ec890.png)
[이미지 출처] https://www.javatpoint.com/merge-sort

```java
public class MergeSort {
    private static int[] tmp;

    private static void merge(int[] arr, int p, int q, int r) {
        int i = p;
        int j = q + 1;
        int t = p;

        while (i <= q && j <= r) {
            if (arr[i] <= arr[j]) {
                tmp[t++] = arr[i++];
            }
            else {
                tmp[t++] = arr[j++];
            }
        }
        // 왼쪽 부분 배열이 남은 경우
        while (i <= q) {
            tmp[t++] = arr[i++];
        }
        // 오른쪽 부분 배열이 남은 경우
        while (j <= r) {
            tmp[t++] = arr[j++];
        }

        // 정렬된 배열을 기존의 배열에 넣기
        i = p; t = p;
        while (i <= r) {
            arr[i++] = tmp[t++];
        }
    }

    private static void mergeSort(int[] arr, int p, int r) {
        if (p < r) {
            int q = (p + r) / 2;
            mergeSort(arr, p, q);
            mergeSort(arr, q + 1, r);
            merge(arr, p, q, r);
        }
    }
    public static void main(String[] args) {
        int[] arr = {10, 5, 2, 23, 45, 21, 7};  
        tmp = new int[arr.length];

        mergeSort(arr, 0, arr.length - 1);

        for(int i : arr){    
            System.out.print(i+" ");    
        } 
    }
}
```
<br>
시간복잡도: Θ(nlogn)    
<br>
시간복잡도가 왜 Θ(nlogn)가 나오는지는 <https://st-lab.tistory.com/233> 에서 자세히 절명하고 있다. 

##### [장점]
* 최악의 경우에도 O(nlogn)이다.
* 안정정렬이다.

##### [단점]
* 정렬과정에서 배열을 하나 더 사용하기에 메모리 사용량이 많다.
* 값을 복사하는 과정에서 데이터가 많을 경우 상대적으로 시간이 많이 소요된다. 

