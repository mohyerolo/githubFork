---
title: 기본적인 정렬 알고리즘(선택, 버블, 삽입)
layout: post
categories: coding
tags: theory
---

정렬 알고리즘은 __단순하지만 비효율적인__  <mark style='background-color: #b6e0dc'> 삽입, 선택, 버블 정렬</mark>   __복잡하지만 효율적인__ 
<mark style='background-color: #b6e0dc'>퀵, 힙, 합병, 기수 정렬</mark> 등으로 나눌 수 있다.    

이 포스팅에서는 단순하지만 비효율적인, 기본적인 정렬 알고리즘을 살펴볼 것이다.     

[1. 선택 정렬 (Selection Sort)](#1.-선택-정렬-(selection-sort))    
[2. 버블 정렬 (Bubble Sort)](#2.-버블-정렬-(bubble-sort))    
[3. 삽입 정렬 (Insertion Sort)](#3.-삽입-정렬-(insertion-sort))

### <mark style='background-color: #fff5b1'> 1. 선택 정렬 (Selection Sort) </mark>   

선택 정렬은 원리가 간단한 정렬 알고리즘 중 하나다.
- 입력에 민감하지 않음
- 항상 일정한 시간복잡도를 가짐
<br>

1. 배열 A[n..1]에서 가장 작은 (큰) 원소를 찾는다. <br>
2. 배열의 처음 (끝)에 있는 A[0] (A[n])과 자리를 바꾼다. <br>
3. 이러면 가장 작은 (큰) 원소는 자기 자리를 찾게된것이다. 이 원소를 제외한 나머지 원소들로 같은 작업을 반복하면 된다. <br>

<br>

```java
public class SelectionSort {
    public static void main(String[] args) {
        int[] arr = {9,14,3,2,43,11,58,22};
        selectionSort(arr, arr.length);

        for(int i:arr){  
            System.out.print(i+" ");  
        }  
    }
    
    private static void selectionSort(int[] arr, int size) {
        // size - 1까지 정렬하면 자동으로 마지막 인덱스는 정렬이 된거임
        for (int i = 0; i < size - 1; i++) {
            int min_index = i;
            // 최솟값을 갖고 있는 인덱스 찾기
            for (int j = i + 1; j < size; j++) {
                if (arr[j] < arr[min_index]) {
                    min_index = j;
                }
            }
            // 최솟값을 갖고 있는 인덱스와 현재 인덱스를 교환
            swap(arr, min_index, i);
        }
    }

    private static void swap(int[] arr, int min_index, int i) {
        // temp에 현재 최솟값을 저장해둠
        int temp = arr[min_index];
        // 최솟값을 갖고있던 원소에 현재 값을 저장
        arr[min_index] = arr[i];
        // 현 원소에 최솟값 저장
        arr[i] = temp;
    }
}
```    

<br>
시간복잡도: O(n<sup>2</sup>)<br>
첫 번째 for문이 n - 1번 순환. 두 번째 for문은 각 부분 배열에서 가장 작은 (큰) 수를 찾는 작업이므로 시간은 부분 배열의 크기에 비례한다
(크기가 k인 배열에서 가장 큰 수를 찾는 데는 k - 1번의 비교가 필요). 부분 배열의 크기는 첫 번째 for문에서 n부터 시작해 2까지 감소한다.    
<br>

그러므로 수를 비교하는 총 횟수는 (n - 1) + (n - 2) + ... + 2 + 1 = n(n - 1) / 2, 즉 O(n<sup>2</sup>)이다.    


##### [장점]
* 추가적인 메모리 소비가 작다.

##### [단점]
* 시간복잡도
* 불안정 정렬이다.
* 100개 이상의 자료에 대해서는 속도가 급격히 떨어져 적절히 사용되기 힘들다.

__정렬 알고리즘의 안정성__ 이란 동일한 키 값을 갖는 레코드들의 상대적인 위치가 정렬 후에도 바뀌지 않는 것을 말한다.    
<br>

그러나 선택 정렬은 같은 인덱스간의 자리를 바꾸며 같은 값일 경우에는 살피지 않기때문에 같은 값일때는 자리를 유지해주지 않는다.
이런 불안정 정렬은 정렬 규칙이 다수이거나 특정 순서를 유지해야 할 때 문제가 될 수 있다.    


<br><br>

### <mark style='background-color: #fff5b1'> 2. 버블 정렬(Bubble Sort) </mark> 

버블 정렬은 제일 큰 원소를 끝자리로 옮기는 작업을 반복한다.    
선택 정렬과 다른 점은 선택 정렬이 가장 큰 수를 찾은 다음 맨 오른쪽 수와 바꾸는 반면, 버블 정렬은 왼쪽부터 이웃한 수를 비교하면서 순서가 제대로 되어 있지 않으면 하나하나 바꾸어나간다.     
그러므로 버블 정렬은 안정 정렬이 될 수 있다.    
<br>

1. 맨 왼쪽부터 시작해 이웃한 쌍과 비교한다. 
2. 현재 원소가 다음 원소보다 크면 자리를 바꾼다.
3. 다음 원소로 이동해 위의 과정을 반복한다.    

<br>

```java
public class BubbleSort {
    private static void bubbleSort(int[] arr, int size) {
        for (int i = 1; i < size; i++) {
            for (int j = 0; j < size - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    swap(arr, j, j + 1);
                }
            }
        }
    }

    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    
    public static void main(String[] args) {
        int arr[] = {3,60,35,2,45,320,5};
        bubbleSort(arr, arr.length);
        for(int i=0; i < arr.length; i++) {  
            System.out.print(arr[i] + " ");
        }
    }
}
```    

<br>
시간복잡도: O(n<sup>2</sup>)    

첫 번째 for문은 n - 1번 순환한다. 두 번째 for문은 i - 1번 순환한다. 선택 정렬과 똑같으므로 O(n<sup>2</sup>)의 시간이 든다는 걸 알 수 있다.    
<br>

그러나 이런 알고리즘은 수행을 시작할 떄나 중간에 배열이 이미 정렬이 되어 있는 상태라도 계속 끝까지 무의미한 순환을 계속한다.    
이를 위해 알고리즘에 한가지를 더할 수 있다.    
<br>

```java
public class BubbleSort_2 {
    private static void bubbleSort(int[] arr, int size) {
        // 왼쪽이랑 비교해야되니까 1부터 시작인것
        for (int i = 1; i < size; i++) {
            boolean sorted = true;
            // i보다 작은것들이랑 비교
            for (int j = 0; j < size - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    swap(arr, j, j + 1);
                    sorted = false;
                }
            }

            /* 바뀌지 않았다는 건 한 번도 교환이 일어나지 않았다는 것
             * 배열이 이미 정렬되어 있는 상태
             */
            if (sorted) break;
        }
    }

    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void main(String[] args) {
        int arr[] = {3,60,35,2,45,320,5};
        bubbleSort(arr, arr.length);
        for(int i=0; i < arr.length; i++) {  
            System.out.print(arr[i] + " ");
        }
    }
}
```
<br>

boolean 값 하나를 정해서 두 번째 for문을 도는 동안 변하는지 살펴볼 수 있게 된다. 중간에 한 번이라도 배열에 교환이 있었다면 
false로 바뀌어 알 수 있게된다. 두 번째 for문을 나왔는데도 바뀌지 않았다면 교환이 한 번도 일어나지 않았다는 것이므로 
배열은 __이미 정렬되어 있는 상태__ 임을 알 수 있다.    
<br>

이렇게 할 경우 배열이 정렬된 상태로 입력되면 버블 정렬은 첫 번째 for문을 한 번만 순환하고 리턴하게 되어 끝난다.    

즉, __O(n)__ 의 시간이 소요된다.    

##### [장점]
* 추가적인 메모리 소비가 작다.

##### [단점]
* 교환 과정이 많아 많은 시간을 소비한다.    


<br><br>

### <mark style='background-color: #fff5b1'> 3. 삽입 정렬(Insertion Sort) </mark>

삽입 정렬은 __이미 정렬되어 있는 i개 짜리 배열__ 에 하나의 원소를 더 더하여 정렬된 i + 1개짜리 배열을 만드는 과정을 반복한다.

1. 현재 원소와 이전의 원소를 비교한다. (처음은 두 번째 원소부터 시작)
2. 현재 원소가 이전 원소보다 작다면 A[i - 1]부터 시작해서 왼쪽으로 훑으며 A[i]가 들어갈 자리를 찾는다.
3. A[i]가 들어가는 자리부터 시작해서 이후의 원소들은 한 칸씩 오른쪽으로 밀린다. 
4. 위와 같은 과정을 마지막 원소까지 반복한다.
<br>

```java
public class InsertionSort {
    private static void insertionSort(int[] arr, int size) {
        for (int i = 1; i < size; i++) {
            int newItem = arr[i];
            int j = i - 1;
            // 이미 정렬된 앞 부분에서 현재 원소보다 큰 게 나오면 그 위치로 들어가야됨
            while (j >= 0 && newItem < arr[j]) {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = newItem;
        }
    }
    public static void main(String[] args) {
        int[] arr = {9,14,3,2,43,11,58,22};
        insertionSort(arr, arr.length);

        for(int i : arr){    
            System.out.print(i+" ");    
        }    
    }
}
```
<br>

시간복잡도: O(n<sup>2</sup>), O(n)    

첫 번째 for문은 n - 1번 순환한다. 매 for문에서 while은 최대 i - 1번 순환한다. 가장 운이 나쁘면 A[i]가 A[0]의 자리에 들어가게 되어 
i - 1번의 순환이 필요하다. 가장 운이 좋으면 A[i]가 제자리에 있게되어 while루프는 한 번도 수행되지 않는다.    
<br>

그러므로 최악의 경우 수행 시간은 1 + 2 + ... + (n - 1) = n(n - 1) / 2로 O(n<sup>2</sup>)가 된다.    
그러나 배열이 거의 정렬되어 있는 상태로 입력되는 경우에는 while루프는 한 번도 수행되지 않을 수 있으므로 O(n)의 시간이 든다.    
<br>

버블 정렬에서는 배열이 이미 정렬되어 있는 경우를 알기위해 변수를 하나 더 사용했다. 그걸로 시간은 줄일 수 있어도 검사하기 위해 사용한 여분의 코드 때문에
오버헤드가 생긴다. 이에 반해 삽입 정렬은 배열이 이미 정렬된 상태라면 그저 while을 돌지 않는 것으로 끝난다.
<br>

##### [장점]
* 추가적인 메모리 소비가 작다.
* 거의 정렬 된 경우 매우 효율적이다. 즉, 최선의 경우 O(N)의 시간복잡도를 갖는다.
* 안정 정렬이다.

##### [단점]
* 역순에 가까울 수록 매우 비효율적이다. 즉, 최악의 경우 O(N2)의 시간 복잡도를 갖는다.
* 데이터의 상태에 따라서 성능 편차가 매우 크다. 







