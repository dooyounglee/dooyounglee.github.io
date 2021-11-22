---
layout: post
title: "[algorithm] 빠진 숫자"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-11-22T23:54:00-04:00
modified: 2021-11-22T23:54:00-04:00
---

# algorithm 빠진 숫자
0부터 n까지 숫자로 이루어진 길이 n짜리 배열에서 빠진 숫자 찾기

## 정렬
시간: O(nlogn)

공간: O(1)

## Hash Table
Hash Table에 기록후 0~n돌면서 없는거 찾기

시간: O(n)

공간: O(n)

## 비트 연산
XOR 연산은 교환법칙 성립.

배열 돌면서 각원소들, 0,1,...,n 모두 XOR연산 하면 똑같은건 0으로 상쇄되고 없는거만 남음.

시간: O(n)

공간: O(1)

## 합, 차
(0~n합) - (배열 원소합) = 빠진 숫자

시간: O(n)

공간: O(1)

