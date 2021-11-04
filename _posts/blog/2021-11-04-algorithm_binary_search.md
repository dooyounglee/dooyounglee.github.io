---
layout: post
title: "[algorithm]이분탐색"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-11-04T23:24:00-04:00
modified: 2021-11-04T23:24:00-04:00
---

# 알고리즘 이분탐색
최대 or 최소값을 예상 범위 안에서 반을 쪼개면서 찾기.

## 전략
최대, 최소 가 될 값의 범위를 찾아서 수직선 상에서 왼쪽(pl), 오른쪽(pr)에 배치

`pl<=pr`인 동안 while문 계속 돌면서 이분탐색

`mid = Math.floor((pl-pr)/2);`

최대 or 최소값이 되고자 하는 값을 mid값으로 가정하면 문제 조건을 만족하는지 확인

mid값으로 가정했을 때 값이 너무 크거나 작거나 문제 조건을 만족할 수 도 있음(당연한 소리)

```
if(mid값이 너무 크다){//예상범위를 반띵해서 앞쪽을 탐색하도록 pr을 땡김
  pr = mid - 1;
}else if(mid값이 너무 작다){//예상범위를 반띵해서 뒷쪽을 탐색하도록 pl을 땡김
  pl = mid + 1;
}else{//문제 조건에 맞는다는 거지만(방심x) 최대 or 최소값을 찾아야 되서 또 찾아야 봐야 함.
  answer = mid;
}
```

여기서 구하는 값이 최대 인지 최소인지에 따라 달라짐

## 최소인 경우
```
if(mid값이 너무 크거나 만족한다){
  pr = mid - 1;
  answer = mid;
}else if(mid값이 너무 작다){
  pl = mid + 1;
}
```

pl, pr을 mid+1, mid-1로 땡기다 보면 pl>pr이 되는 순간이 올텐데, 이때 while문을 빠져나감
