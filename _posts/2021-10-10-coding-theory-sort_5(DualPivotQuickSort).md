---
title: Dual-Pivot Quick Sort
layout: post
categories: coding
tags: theory
---
정렬을 할 수 있는 Arrays.sort()는 Insertion Sort와 Quick Sort를 섞은 Dual-Pivot Quick Sort, Insertion Sort와 Merge Sort를 섞은 Tim Sort를 사용한다.  

지금은 Insertion Sort를 합치지 않은 Dual-Pivot Quick Sort를 알아볼 것이다.    

## Dual-Pivot Quick Sort
__Dual-Pivot Quick Sort__ 는 퀵소트를 변형한 정렬 중 하나로 퀵소트의 장점을 극대화하여 평균적인 연산량을 더 줄여내도록 만들었다.   
이론적, 실험적으로 랜덤 데이터에 대해 보통의 Quick Sort보다 상당히 좋은 것으로 판명되었으나 여전히 최악의 경우 시간 복잡도는 O(N<sup>2</sup>)이다. 

Dual-Pivot이므로 partitioning을 할 때 Pivot을 하나가 아닌 두 개로 잡는다.    

![image](https://user-images.githubusercontent.com/68698007/136683761-24e27712-df58-4a00-8746-bd25789a56cf.png)
[이미지 출처] http://www.secmem.org/blog/2019/05/06/special-sorts-2/


각 pivot은 제일 왼쪽의 값, 오른쪽의 값이 되고 이 값들을 중심으로    
1. x < 첫 번째 Pivot  
2. 첫 번째 Pivot <= x <= 두 번째 Pivot    
3. 두 번째 Pivot < x    

총 세 개의 범위로 나뉜다.    

이렇게 세 개의 범위로 나누기 위해서는 아래의 변수들이 사용된다.
1. __lp__ : 왼쪽 Pivot의 값

2. __l__ : 왼쪽 pivot이 나중에 들어갈 인덱스(왼쪽 Pivot보다 작은 값들의 인덱스를 알 수 있음).     
왼쪽 pivot이 나중에 들어간다는 것은 알고리즘이 진행하면서는 _왼pivot보다 작은 값이 들어갈 다음 위치_ 를 가지고 있다는것이다. l은 k가 진행되면서 왼쪽에 들어갈 값을 찾을 경우 arr[k]와 arr[l]을 교환하는데 쓰인다.

3. __k__ : 현재 인덱스(모든 요소를 검사할). 왼쪽 pivot + 1의 값으로 시작해 배열에 담겨있는 원소들을 검사하며 값이 들어갈 위치를 변경한다.

4. __rp__ : 오른쪽 Pivot의 값

5. __r__ : 오른쪽 pivot이 나중에 들어갈 인덱스(오른쪽 Pivot보다 큰 값들의 인덱스).    
l과 같은 역할을 한다. _오른쪽 pivot보다 큰 값이 들어갈 다음 위치_ 를 가지고 있다. k가 rp보다 큰 값을 찾게 될 경우 arr[k]와 arr[r]를 바꾸는데 쓰인다.    

```java
public class DualPivotQuickSort {
    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    private static void dualPivotQuickSort(int[] arr, int left, int right) {
        if (left < right) {
            if (arr[left] > arr[right]) {
                swap(arr, left, right);
            }
    
            int lp = arr[left];
            int rp = arr[right];
    
            int l, k, r;
            l = k = left + 1;
            r = right - 1;
    
            /**
             * rp보다 큰 값이 들어갈 자리인 r변수와, 현재 인덱스를
             * 비교하는 k변수가 교차되면 모든 인덱스에 대한 검사를 마친 것
             */
                while (k <= r) {
                    if (arr[k] < lp) {
                        swap(arr, k, l);
                        l++;
                    }
                    else if (arr[k] > rp) {
                        /**
                         * k < r: 아직 모든 요소의 검사가 끝나지 않음
                         * r은 rp보다 큰 값이 들어갈 다음 자리를 가리키는 인덱스이므로
                         */
                        while ((arr[r] > rp) && k < r) {
                            r--;
                        }
                        swap(arr, k, r);
                        r--;
    
                        if (arr[k] < lp) {
                            swap(arr, k, l);
                            l++;
                        }
                    }
                k++;
            }
    
            // 두 개는 각자 다음의 위치를 가리키므로 밑의 과정이 필요
            l--;
            r++;
            swap(arr, left, l);
            swap(arr, right, r);
    
            dualPivotQuickSort(arr, left, l - 1);
            dualPivotQuickSort(arr, l + 1, r - 1);
            dualPivotQuickSort(arr, r + 1, right);
        }
    }

    public static void main(String[] args) throws Exception {
        int[] arr = { 4, 2, 5, 3, 6, 10, 9, 8, 7};
        dualPivotQuickSort(arr, 0, arr.length - 1);

        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

참고 블로그    
<https://cs-vegemeal.tistory.com/53>    
<https://defacto-standard.tistory.com/38>    
<http://www.secmem.org/blog/2019/05/06/special-sorts-2/>
