---
layout: post
title: "[algorithm] prob2"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-11-10T22:57:00-04:00
modified: 2021-11-10T22:57:00-04:00
---

# algorithm 정렬된 두 배열 병합
두 배열 nums1, nums2. nums1의 크기는 병합하기 충분

## 합쳐서 sort
시간: O(nlogn) (∵ 내부적으로 Timsort)

공간: O(n)

Timesort: 최선_O(n), 평균_O(nlogn), 최악_O(nlogn), 공간_O(n)

## 각 배열 포인터로 넘기면서
p1, p2로 두고 nums1[p1]이랑 nums2[p2]를 비교하면서 넣고 넣은 포인터+1

```
var nums1 = [1,2,3,0,0,0];var len1 = 3;
var nums2 = [2,5,6];var len2 = 3;
let p1 = len1-1;
let p2 = len2-1;
let p = len1 + len2 - 1;

while(p >= 0){
	if(nums1[p1] <= nums2[p2]){
    nums1[p] = nums2[p2];
    p--;
    p2--;
  }else{
    nums1[p] = nums1[p1];
    p--;
    p1--;
  }
}
console.log(nums1);
```
시간: O(n+m)

공간: O(1)
