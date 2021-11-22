---
layout: post
title: "[algorithm] 과반수 찾기"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-11-22T23:27:00-04:00
modified: 2021-11-22T23:27:00-04:00
---

# algorithm 과반수찾기
Math.floor(n/2) 초과 인 수 찾기

## 2중 for문


## Hash Table
arr를 돌면서 map에 기록하는데, 없는 키값이면 value값1, 있는 키값이면 value값+1

초과인 key return.

```
var arr=[8,2,2,2,7,2];
var map={};
let num=Math.floor(arr.length/2)+1;

for(let x of arr){
	if(map[x]==undefined)map[x]=1;
	else map[x]++;
	
	if(map[x]>=num){
		console.log(x);break;
	}
}
```
시간: O(n)

공간: O(n)

## 정렬ㄷㄷ
정렬하고 가운데 원소 return;

시간: O(nlogn)

공간: O(1)
