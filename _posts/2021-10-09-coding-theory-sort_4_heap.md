---
title: 힙 정렬 (Heap Sort)
layout: post
categories: coding
tags: theory
---
__힙 정렬__ 은 힙 자료구조를 사용하는 정렬 알고리즘이다. 그러므로 힙 정렬을 다루기 전에 힙에 대해 자세히 알고있어야 한다.    

## 힙 (Heap)
힙은 이진트리로 맨 아래 층을 제외하고는 완전히 채워져 있고 맨 아래는 왼쪽부터 채워져 있다. 힙에는 <mark style='background-color: #fff5b1'>최대힙</mark>과 <mark style='background-color: #fff5b1'>최소힙</mark>이 있고 그에따라 설명이 조금은 달라지지만 그저 큰 걸 올리냐, 작은 걸 올리냐의 문제일뿐이다. 교재에서는 최소힙으로 설명을 했지만 검색 결과 대부분 최대힙으로 하더라.. 가능하면 둘 다 구현해보겠다.    


최소힙은 __각 노드의 값은 자기 자식의 값보다 작거나 같다__ 의 성질을 만족해야한다. 즉, 최소힙의 루트 노드에서 최솟값이 자리하게 된다.    
최대힙은 __각 노드의 값은 자기 자식의 값보다 크거나 같다__ 의 성질을 만족해야 되는 것이다. 최소힙과 다르게 최대힙은 루트 노드에 최댓값이 자리하게 된다.    

결국 __부모 노드는 자식노드보다 항상 우선순위가 앞서는 노드__ 라는 것이다.    

(a)
<img src = "https://user-images.githubusercontent.com/68698007/136571591-95925f68-41c3-4009-bb01-0c6071dbe5f5.png" width = 200 height = 200>
(b)
<img src = "https://user-images.githubusercontent.com/68698007/136572110-cb545da9-0f67-4a18-8ccc-978b61bec38b.png" width = 210 height = 210>
(c)
<img src = "https://user-images.githubusercontent.com/68698007/136572875-5020e2cf-1d21-429a-a9b8-91843a18bf61.png" width = 190 height = 190>

그림에서 (b)는 제일 왼쪽에서부터 채워지지 않았으므로 구조상 힙이 아니다. (c)는 왼쪽에서부터 채워지지 않았으며 루트 노드가 최솟값이 아니므로 최소힙의 성질을 만족하지 못 한다. 결국 셋 중 최소힙인 것은 (a)이다.    

(a)에서 볼 수 있듯이 형제 노드간의 우선순위는 비교하지 않고 부모와 자식 간의 관계만 신경쓰기 때문에 __반 정렬 상태__, __느슨한 정렬 상태__ 혹은 __약한 힙__ 이라고도 한다.  

힙 정렬은 이런 힙의 성질을 이용해서 정렬하는 것이다.    
<br><br><br>


## 힙 정렬 (Heap Sort)

힙 정렬은 먼저 주어진 배열을 힙으로 만든 후, 힙에서 가장 작은 값(최소힙일 경우 루트 노드)을 하나씩 제거하면서 힙의 크기를 줄여나가면 힙 정렬이 된다.        

힙은 꽉 찬 이진 트리이므로 배열로 쉽게 표현할 수 있다.    

- 왼쪽 자식 노드: A[부모노드 * 2] + 1
- 오른쪽 자식 노드: A[부모노드 * 2] + 2
- 부모 노드: A[현재노드 - 1 / 2]

<br>

<img src = "https://user-images.githubusercontent.com/68698007/136571591-95925f68-41c3-4009-bb01-0c6071dbe5f5.png" width = 200 height = 200>

위에서 본 그림을 배열로 표현하면 {3, 6, 4, 8, 9}가 된다.    

<br>

힙을 정렬하는거는 우선순위 큐를 사용하는 방법이 있다. 그러나 이 방법은 간단하지만 따로 클래스를 가져와야되므로 비효율적이다.

```java
import java.util.PriorityQueue;

public class HeapSort_PriorityQueue {
    public static void main(String[] args) {
        int[] arr = { 7, 9, 4, 8, 6, 3 };
        
        PriorityQueue<Integer> heap = new PriorityQueue<Integer>();

        // 배열을 힙으로
        for (int i = 0; i < arr.length; i++) {
            heap.add(arr[i]);
        }

        // 힙에서 우선순위가 가장 높은 원소를 뽑아냄
        for (int i = 0 ; i < arr.length; i++) {
            arr[i] = heap.poll();
        }

        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```
PriorityQueue를 사용하면 발생하는 메모리를 아끼기 위해 위에서 적은 것처럼 기존 배열을 힙으로 만들고 정렬하면 된다.    

## 최대힙 정렬
### 1. 힙으로 만들기    
- 맨 마지막 노드를 형제 노드와 비교해 제일 큰 값을 가진 노드를 고르고 그 노드의 부모 노드와 비교해 힙 성질을 만족하는지 확인한다.
- 만족하지 못 하면 값을 교환한다.
- 교환된 값이 현 노드의 자식 노드들과 힙 성질을 만족하는지 확인한다.
- 만족하지 못 하면 값을 교환한다. 

위의 방법을 A([n / 2])부터 A(1)까지 차례로 루트로 삼아 총 __[n / 2]번__ 을 수행하게 된다.    

```java
public class HeapSort_max {
    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void heapify(int[] arr, int k, int n) {
        int left = 2 * k + 1;
        int right = 2 * k + 2;
        int largest = k;
        
        if (right <= n && arr[largest] < arr[right]) {
            largest = right;
        }
        if (left <= n && arr[largest] < arr[left]) {
            largest = left;
        }
        
        /**
         * largest != k는 largest의 값이 변경됐다는 것이므로
         * 부모 노드보다 큰 값이 자식 노드에 있다는 것.
         */
        if (largest != k) {
            swap(arr, largest, k);
            heapify(arr, largest, n);
        }
    }

    public static void buildHeap(int[] arr, int n) {/
        // 현재 노드의 부모 노드부터
        for (int i = n / 2; i >= 0; i--){
            heapify(arr, i, n);
        }
    }

    public static void heapSort(int[] arr, int n) {
        buildHeap(arr, n);
    }

    public static void main(String[] args) {
        int[] arr = { 3, 7, 5, 4, 2, 8 };

        heapSort(arr, arr.length - 1);
        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

### 2. 정렬하기
- 현재 루트 노드에는 최댓값이 저장되어 있다. 루트 노드의 값을 제일 마지막 노드의 값과 바꾸면 최댓값이 제일 뒤로 가게 된다.
- 바뀐 루트 노드를 중심으로 다시 힙성질을 만족하도록 heapify() 실행

```java
public class HeapSort_max {
    /**
     * 위와 동일함
     */

    public static void heapSort(int[] arr, int n) {
        buildHeap(arr, n);

        // 제일 마지막 노드에서부터 루트 노드전까지 반복
        for (int i = n; i > 0; i--) {
            // 루트와 현재 노드를 바꾼다. -> 큰 값들이 뒤로 가는 것
            swap(arr, 0, i);
            // 힙성질을 지키도록 현재 바꾼 노드 전까지 수정 -> 루트 노드에 다시 최댓값이 올라감
            heapify(arr, 0, i - 1);
        }
    }

    public static void main(String[] args) {
        int[] arr = { 3, 7, 5, 4, 2, 8 };

        heapSort(arr, arr.length - 1);
        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

이 방법을 통해 최대힙으로 정렬이 완료된다.    

그러나 이런 재귀방식은 최악의 경우 트리의 높이만큼 재귀가 발생해 StackOverFlow가 발생할 수 있다. 재귀를 사용하지 않고 반복문으로도 구현할 수 있다.    

```java
public class HeapSort_max_2 {
    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void heapify(int[] arr, int k, int n) {
        int left;
        int right;
        int largest;
        
        while ((k * 2) + 1 <= n) {
            left = k * 2 + 1;
            right = k * 2 + 2;
            largest = k;

            if (right <= n && arr[largest] < arr[right]) {
                largest = right;
            }

            if (arr[largest] < arr[left]) {
                largest = left;
            }
            
            /**
             * largest != k는 largest의 값이 변경됐다는 것이므로
             * 부모 노드보다 큰 값이 자식 노드에 있다는 것.
             */
            if (largest != k) {
                swap(arr, largest, k);
                k = largest;
            }
            else {
                return;
            }
        }
    }

    public static void buildHeap(int[] arr, int n) {
        for (int i = n / 2; i >= 0; i--){
            heapify(arr, i, n);
        }
    }
    
    public static void heapSort(int[] arr, int n) {
        buildHeap(arr, n);
        // 제일 마지막 노드에서부터 루트 노드전까지 반복
        for (int i = n; i > 0; i--) {
            // 루트와 현재 노드를 바꾼다. -> 큰 값들이 뒤로 가는 것
            swap(arr, 0, i);
            // 힙성질을 지키도록 현재 바꾼 노드 전까지 수정 -> 루트 노드에 다시 최댓값이 올라감
            heapify(arr, 0, i - 1);
        }
    }

    public static void main(String[] args) {
        int[] arr = { 3, 7, 5, 4, 2, 8 };

        heapSort(arr, arr.length - 1);
        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

<br>
<br>

## 최소힙 정렬
최소힙은 최대힙과 다르게 제일 작은 값, 최솟값이 루트로 올라간다.   
그 외의 것은 최대힙과 다르지 않다. 
- 맨 마지막 노드를 형제 노드와 비교해 제일 작은 값을 가진 노드를 고르고 그 노드의 부모 노드와 비교해 힙 성질을 만족하는지 확인한다.
- 만족하지 못 하면 값을 교환한다.
- 교환된 값이 현 노드의 자식 노드들과 힙 성질을 만족하는지 확인한다.
- 만족하지 못 하면 값을 교환한다. 

```java
public class HeapSort_min {
    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void heapify(int[] arr, int k, int n) {
        int left = 2 * k + 1;
        int right = 2 * k + 2;
        int largest = k;
        
        if (right <= n && arr[largest] > arr[right]) {
            largest = right;
        }
        if (left <= n && arr[largest] > arr[left]) {
            largest = left;
        }
        
        /**
         * largest != k는 largest의 값이 변경됐다는 것이므로
         * 부모 노드보다 큰 값이 자식 노드에 있다는 것.
         */
        if (largest != k) {
            swap(arr, largest, k);
            heapify(arr, largest, n);
        }
    }

    public static void buildHeap(int[] arr, int n) {
        for (int i = n / 2; i >= 0; i--){
            heapify(arr, i, n);
        }
    }

    public static void heapSort(int[] arr, int n) {
        buildHeap(arr, n);
        for (int i = n; i > 0; i--) {
            swap(arr, 0, i);
            heapify(arr, 0, i - 1);
        }
    }
    public static void main(String[] args) {
        int[] arr = { 3, 7, 5, 4, 2, 8 };

        heapSort(arr, arr.length - 1);
        for (int i = arr.length - 1; i >= 0; i--) {
            System.out.print(arr[i] + " ");
        }
    }
}
```

최소힙은 힙을 만들고 정렬을 하면 배열에 역순(내림차순)으로 정리가 된다. 그래서 출력할때 거꾸로 출력을 해야 오름차순으로 나온다.    
<br>
<br>

시간 복잡도: <mark style='background-color: #fff5b1'>O(nlogn)</mark>

buildHeap()에는 Θ(n)의 시간이 소요된다.    
-> heapify()는 해당 서브 트리의 높이가 시간을 좌우한다. 어떤 서브 트리도 높이가 logN을 넘지 않으므로 heapify()를 한 번 수행하는데 O(logN)이 소요된다. 그러나 이건 과하게 잡은 상한이다. 맨 처음에 호출되는 heapify()의 입력 트리는 높이가 고작 1이고 올라갈수록 높이가 높은 부분 트리의 수는 줄어든다. 이 경우들을 합산하면 O(nlogn)이 아닌 Θ(n)이 된다.    

heapSort()의 for문에서는 n-1번 순환하고 heapify()는 충분히 잡아서 O(logn)이면 된다.    

그러므로 힙 정렬의 총 수행 시간은 O(nlogn)이다.

<br>
<br>

##### [장점]
* 최악의 경우에도 O(nlogn)

##### [단점]
* 힙을 만들면서 불안정 정렬 상태에서 최대 / 최소의 값만 갖고 정렬을 하기 때문에 불안정 정렬이다.
