---
title: Tim Sort(수정필요)
layout: post
categories: coding
tags: theory
---
__Tim Sort__ 는 앞에서 작성한 Dual-Pivot Quick Sort같이 Arrays.sort()의 기본 알고리즘으로 채택됐다. 이는 Insertion Sort와 Merge Sort가 합쳐진 것으로 여기서 사용하는 Insertion Sort는 선형 탐색이 아닌 __이진 탐색(이분 탐색)__ 을 적용한 __Binary Insertion Sort__ 를 사용한다. 이분 탐색은 타겟이 들어갈 자리를 받아와 비교 하는 작업이 없이 타겟의 위치까지만 옮겨주면 된다. 그러나 타겟이 들어갈 자리를 받아오기 위해 실행하는 과정때문에 일반적인 정렬에서는 Insertion Sort보다 약간은 느리지만 객체를 정렬하고자 할 때(여러 개를 비교해야 할 경우)는 Insertion Sort보다 빠른 정렬을 보여준다.

Arrays.sort()에서 primitive type 일차원 배열의 경우 Dual-Pivot Quick Sort를 사용하면 되고 객체를 정렬하고자 할 때는 Time Sort를 사용하는 것이다.

## Tim Sort
