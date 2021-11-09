---
layout: post
title: "[algorithm] prob1"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-11-09T23:17:00-04:00
modified: 2021-11-09T23:17:00-04:00
---

# algorithm 배열의 두 원소의 합이 특정값이 되는 경우 찾기
`nums = [2,7,10,19]` `target = 9`

## 2중 for문
시간: O(n^2)

공간: O(1)

## HashTable
`target - 원소` 를 hashTable에 없으면 키값으로, value는 index로
```
var nums = [2,7,10,19];
var target = 9;
let obj = {};

for(let i = 0; i < nums.length; i++){
	let diff = target - nums[i];
	if(obj[diff] === undefined){
		obj[nums[i]] = i;
	}else{
		console.log(i,obj[diff]);
		break;
	}
}
```
시간: O(n)

공간: O(n). 해시 테이블을 생성하여 최대 n개를 
