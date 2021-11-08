---
layout: post
title: "[oracle] KEEP"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-11-08T23:25:00-04:00
modified: 2021-11-08T23:25:00-04:00
---

# ORACLE KEEP
그룹함수의 값인 다른 행값 가져오기.

## KEEP 없이
SAL 최대인 ID를 가져오려면
```
SELECT ID FROM TABLE
WHERE SAL = (SELECT MAX(SAL) FROM TABLE);
```

## KEEP 이용
```
SELECT MAX(ID) KEEP(DENSE_RANK FIRST ORDER BY SAL DESC) FROM TABLE
```
