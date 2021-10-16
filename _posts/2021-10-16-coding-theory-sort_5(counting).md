---
title: Counting Sort
layout: post
categories: coding
tags: theory
---
## Counting Sort (계수 정렬)
__카운팅 정렬__ 은 주어진 배열에 있는 원소들의 각 빈도수를 저장한 배열 하나를 더 만들고, 그 배열을 이용해 정렬하는 알고리즘이다.    

따라서 카운팅 정렬에서는 _배열의 최댓값을 찾아 최댓값의 크기만한 배열을 만들어야 된다_ (배열의 크기: 최댓값 + 1, 최댓값을 포함해야하므로).    

순서에 대한 그림과 자세한 설명은
<https://www.programiz.com/dsa/counting-sort>
여기에 적혀있다.    

최댓값만큼의 공간을 할당해야하므로 만약에 10개의 숫자가 주어졌는데 그 범위가 1 ~ 1억이라면 10개의 수를 정렬하기 위해 1억개의 공간을 할당해야되는것이다. 그러므로 Counting Sort는 각 원소의 범위가 그렇게 크지 않을 경우에는 매우 빠르나 범위가 크다면 메모리 낭비가 심하고, 자바에서는 1차원 배열 객체 하나의 크기는 최대 Integer.MAX_VALUE 미만으로만 가능하기 때문에 실생활에서는 거의 안 쓰인다.    

```java
public class CountingSort {
    private static int getMax(int[] arr) {
        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (max < arr[i]) {
                max = arr[i];
            }
        }
        return max;
    }
    private static void countingSort(int[] arr, int n) {
        int size = getMax(arr);
        /** counting배열은 값을 보기 위한 배열로 
         * 값이 10까지 있으면 counting[10]도 존재해야하므로
         * 공간을 11개 확보해야됨.
         * 즉, 최댓값 + 1의 공간 할당이 필요.
         */
        int[] counting = new int[size + 1];
        // 기존 배열인 arr에 정렬된 값을 넣기위해 필요한 배열
        int[] output = new int[n];

        /**
         * arr[i]의 값을 counting배열의 index로 취급해 값을 하나씩 증가시킨다. 
         * counting[7]이 0이면 arr배열에 7인 원소는 없는 것. 
         * counting[3]이 2면 arr배열에 3이 두 개 있는 것이다.
         */
        for (int i = 0; i < n; i++) {
            counting[arr[i]]++;
        }

        /**
         * 원래 배열에 값을 넣을 때 위치를 찾기 위해 counting 배열의 값을 더하는 것.
         * counting[0] = 1, counting[1] = 3, counting[2] = 3, counting[3] = 4이면
         * arr배열에서 0이 하나 있어서 0이 arr배열의 첫 번째 위치(인덱스 0)로
         * 가야됨. 1인 원소는 2개 있는 것으로 보고 각각 arr배열에서 인덱스 1, 2 위치로 가야됨.
         * counting[2]는 counting[1]과 값이 다르지 않음. 2가 없다는 것.
         * counting[3]이 4가 됐으므로 3이 하나 존재하고 인덱스 3으로 가야됨.
         * 이걸 알기 위해 각 값을 더하는 것.
         */
        for (int i = 1; i < counting.length; i++) {
            counting[i] += counting[i - 1];
        }

        /**
         * 정렬 안정성을 유지하기위해 맨 뒤에서부터 보는 것.
         * --counting[arr[i]]: counting배열의 값이 위치를 가지고 있으므로
         * arr크기만한 배열에 넣기위해서는 -1을 해줘야됨.
         * 
         * counting[9] = 8이면
         * arr[i]가 9일때
         * --counting[9]은 7이 되고 output[7]에 9가 들어가는 것이다.
         */
        for (int i = n - 1; i >= 0; i--) {
            output[--counting[arr[i]]] = arr[i];
        }

        for (int i = 0; i < n; i++) {
            arr[i] = output[i];
        }
    }
    public static void main(String[] args) {
        int[] arr = { 4, 2, 5, 3, 6, 10, 9, 8, 7};
        countingSort(arr, arr.length);

        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```    

시간복잡도: O(n)

#### 장점
- O(n)의 시간복잡도
- 안정 정렬
- 작은 범위의 수를 정렬할때는 매우 빠름

#### 단점
- 범위가 커질수록 메모리 낭비가 심해짐
