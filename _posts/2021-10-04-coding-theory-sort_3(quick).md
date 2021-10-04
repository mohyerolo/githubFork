---
title: 퀵 정렬 (Quick Sort)
layout: post
categories: coding
tags: theory
---
퀵 정렬은 평균적으로 가장 좋은 성능을 가졌다.    
퀵 정렬도 병합 정렬처럼 분할 정복 방법을 사용한다. 병합 정렬과 다른 부분은 리스트를 <mark style='background-color: #fff5b1'>비균등 분할</mark>한다는 것과 <mark style='background-color: #fff5b1'>불안정 정렬</mark>이라는 것이다. 

## 퀵 정렬 (Quick Sort)
1. 리스트에서 하나의 기준 원소(pivot)를 잡는다.
2. 기준 원소를 중심으로 작거나 같은 수는 왼쪽으로, 큰 수는 오른쪽으로 재배치한다. 
3. 부분리스트를 정렬한다.
4. 위의 과정을 반복한다.

위에서 반으로 나눠서 부분리스트를 만드는 것이 아닌 임의의 기준 원소를 정하므로 비균등 분할이 되는 것이다. 또한 하나의 피벗을 두고 두 개의 부분 리스트를 만들 때 서로 떨어진 원소끼리 교환이 일어나기때문에 불안정 정렬이 된다.    


Pivot을 설정하는 기준은 보통 제일 왼쪽 or 오른쪽 or 중간이다. 각 방법에 따라 코딩도 조금씩 달라진다.    

<br>

### <mark style='background-color: #fff5b1'>왼쪽 pivot 선택</mark>
1. 왼쪽 pivot을 선택하는 첫 번째 방법으로 교재에서 배웠던 걸 써봤다.    

제일 왼쪽 값이 pivot이 되므로 i는 제일 왼쪽 값부터, j는 왼쪽 값보다 하나 앞의 인덱스부터 시작한다. 그리고 만약 a[j]의 값이 pivot보다 작다면 i의 값을 증가시키고 i와 j를 swap한뒤 j의 값을 증가시킨다.    

i는 pivot이 들어갈 인덱스가 되어가는거고 j는 처음부터 끝까지 훑는 용도로 사용하게 된다. 

```java
public class QuickSort_left {
    private static void swap(int[] a, int i, int j) {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
    private static int partition(int[] a, int p, int r) {
        int pivot = a[p];
        int i = p;

        for (int j = p + 1; j < r + 1; j++) {
            if (a[j] < pivot) {
                swap(a, ++i, j);
            }
        }
        swap(a, p, i);

        return i;
        
    }

    private static void quickSort(int[] a, int p, int r) {
        if (p < r) {
            int q = partition(a, p, r);
            quickSort(a, p, q - 1);
            quickSort(a, q + 1,  r);
        }
    }
    public static void main(String[] args) {
        int a[] = { 13, 18, 27, 2, 19, 25 };  
        quickSort(a, 0, a.length - 1);
        for(int i : a){  
            System.out.print(i+" ");  
        }
    }
}
```
<br>

2. 블로그에서 본 방법을 사용해봤다.    

<https://st-lab.tistory.com/250>

제일 오른쪽 부터 pivot보다 작은 값이 나올 때까지 인덱스를 감소시킨다.    
pivot보다 작은 값을 찾으면 pivot + 1 인덱스부터 pivot보다 큰 값이 나올 때까지 인덱스를 증가시킨다.    
각 경계값을 서로 바꿔주고 다시 위의 과정을 반복한다.    
__작은 값의 인덱스 < 큰 값 인덱스__ 를 만족하지 못하면 pivot과 작은 값의 인덱스의 원소를 바꿔준다.    

pivot을 기준으로 왼쪽과 오른쪽 부분리스트로 쪼개서 위의 과정을 반복하면 된다.    

이 과정을 통해 pivot의 값이 정렬됐을 때 들어가야 되는 자신의 자리로 들어가게 된다. 

```java
public class QuickSort_left2 {
    private static void swap(int[] a, int i, int j) {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
    private static int partition(int[] a, int p, int r) {
        int pivot = a[p];
        int i = p;
        /**
         * i의 인덱스가 p + 1이 아닌 p인 이유는
         * 비교 값이 두 개(pivot과 pivot + 1인덱스에 있는 원소)일때
         * i < j를 만족시키지 못하므로 루프가 수행되지 않는다.
         * 그렇게되면 pivot값이 pivot + 1 인덱스의 값보다 클 때 정렬이 되지 않음
         */
        int j = r;

        while (i < j) {
            while (a[j] > pivot && i < j) {
                j--;
            }
            while (a[i] <= pivot && i < j) {
                i++;
            }
            swap(a, i, j);
        }
        swap(a, p, i);

        return i;
    }

    private static void quickSort(int[] a, int p, int r) {
        if (p < r) {
            int q = partition(a, p, r);
            quickSort(a, p, q - 1);
            quickSort(a, q + 1,  r);
        }
    }
    public static void main(String[] args) {
        int a[] = { 13, 18, 27, 2, 19, 25 };  
        quickSort(a, 0, a.length - 1);
        for(int i : a){  
            System.out.print(i+" ");  
        }
    }
}
```

<br>

### <mark style='background-color: #fff5b1'>오른쪽 pivot 선택</mark>

1. 교재

왼쪽 pivot과 같은 방식으로 i 인덱스는 p - 1값부터 시작해 pivot이 들어갈 자리를 찾고, j는 처음부터 끝까지 훑으며 pivot보다 작은 값이면 i의 인덱스가 증가하고 a[i]와 a[j]를 바꿔준다. 이때 a[i]는 이미 a[j]로 훑고 지나간 자리로 pivot보다 작을 수가 없다.    

```java
public class QuickSort_right {
    private static void swap(int[] a, int i, int j) {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
    private static int partition(int[] a, int p, int r) {
        int pivot = a[r];
        int i = p - 1;

        for (int j = p; j < r; j++) {
            if (a[j] < pivot) {
                swap(a, ++i, j);
            }
        }
        swap(a, r, i + 1);

        return i;
    }

    private static void quickSort(int[] a, int p, int r) {
        if (p < r) {
            int q = partition(a, p, r);
            quickSort(a, p, q - 1);
            quickSort(a, q + 1,  r);
        }
    }
    public static void main(String[] args) {
        int a[] = { 13, 18, 27, 2, 19, 25 };  
        quickSort(a, 0, a.length - 1);
        for(int i : a){  
            System.out.print(i+" ");  
        }
    }
}
```

2. 블로그에서 본 방법

```java
public class QuickSort_right2 {
    private static void swap(int[] a, int i, int j) {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
    private static int partition(int[] a, int p, int r) {
        int pivot = a[r];
        int i = p;
        int j = r;

        while (i < j) {
            /**
             * left pivot때와 다르게 i부터 수행하는 이유는 j부터 비교하게되면
             * pivot의 값이 배열에서 제일 큰 값일 경우
             * a[j] >= pivot으로인해 j는 하나 작은 인덱스가되지만
             * 바뀐 인덱스 j의 원소(pivot인덱스 - 1)가 pivot보다 큰 값이 
             * 아님. 그럼에도 j부터 수행하고 i를 구하게되면 i < j 때문에
             * i가 pivot - 1의 인덱스를 가질 수밖에 없게된다.
             * 그렇게 되면 최댓값이 맨 끝에 위치하지 못하게 됨.
             */
            while (a[i] < pivot && i < j) {
                i++;
            }
            while (a[j] >= pivot && i < j) {
                j--;
            }
            swap(a, i, j);
        }
        swap(a, r, j);

        return j;
    }

    private static void quickSort(int[] a, int p, int r) {
        if (p < r) {
            int q = partition(a, p, r);
            quickSort(a, p, q - 1);
            quickSort(a, q + 1,  r);
        }
    }
    public static void main(String[] args) {
        int a[] = { 13, 18, 19, 2, 25, 27 };  
        quickSort(a, 0, a.length - 1);
        for(int i : a){  
            System.out.print(i+" ");  
        }
    }
}
```
<br>

### <mark style='background-color: #fff5b1'>중간 pivot 선택</mark>
1. 블로그에서 본 방법

```java
public class QuickSort_mid {
    private static void swap(int[] a, int i, int j) {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
    private static int partition(int[] a, int p, int r) {
        int i = p - 1;
        int j = r + 1;
        int pivot = a[(p + r) / 2];

        while (true) {
            do {
                i++;
            } while (a[i] < pivot);

            do {
                j--;
            } while (a[j] > pivot && i <= j);

            /**
             * i >= j라는 것은 i는 이미 증가할 수 있을만큼 증가했고
             * j의 값이 i를 지나쳤다는 것이다. 이는 pivot보다 큰 값이
             * 없다는 것이다.
             */
            if (i >= j) {
                return j;
            }

            swap(a, i, j);
        }
    }

    private static void quickSort(int[] a, int p, int r) {
        if (p < r) {
            int q = partition(a, p, r);
            quickSort(a, p, q);
            quickSort(a, q + 1,  r);
        }
    }
    public static void main(String[] args) {
        int a[] = { 5, 3, 8, 9, 2, 4, 7 };  
        quickSort(a, 0, a.length - 1);
        for(int i : a){  
            System.out.print(i+" ");  
        }
    }
}
```

<br><br>
시간복잡도: Θ(nlogn)    
<br>
시간복잡도가 왜 Θ(nlogn)가 나오는지는 

<https://st-lab.tistory.com/250> 에서 자세히 설명하고 있다. 

##### [장점]
* 최악의 경우에도 O(nlogn)이다.
* 메모리를 적게 소비한다.

##### [단점]
* 왼쪽, 오른쪽 pivot을 선택한 경우 정렬 된 상태의 배열을 정렬하고자 할 때는 한 쪽의 부분리스트에는 아무 것도 없이 한 쪽에 다 몰리도록 분할된다. 이럴 경우에는 각 재귀에서 N개의 비교작업을 N번 호출하기 때문에 O(n<sup>2</sup>)의 성능을 내기도 한다. 이는 중간값을 pivot으로 선택하면 불균등 분할 완화가 가능하다.    
