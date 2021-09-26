---
title: 병합 정렬(Merge Sort)
layout: post
categories: coding
tags: theory
---
기본적인 정렬 알고리즘은 모두 평균 Θ(n<sup>2</sup>)의 시간이 소요된다. 앞으로 포스팅할 정렬 알고리즘은 모두 평균 
Θ(nlogn)의 시간이 소요된다.    

병합 정렬의 경우 최악의 경우에도 Θ(nlogn)이 소요된다.    

### 병합 정렬(Merge Sort)
1. 리스트를 두 개의 균등한 크기로 분할하고 분할된 부분리스트를 정렬
2. 정렬된 두 개의 부분리스트를 합하여 전체 리스트 정렬

병합 정렬의 정렬 과정은 위와 같다. 이런 방법을 분할 정복(divide and conquer)방법이라고 한다.    

