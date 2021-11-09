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
modified: 2021-11-09T23:52:00-04:00
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

## 근데 KEEP은 scalar값
KEEP의 결과는 scalar여서 record전체를 가져오려면 필요한 col수 만큼 KEEP을 써야 하는듯.

대신 ROW_NUMBERS() 의 1번만 가져오도록 한다면?

`SELECT COL1, COL2, COL3, COL4 FROM TABLE` 에서 COL3에서 MAX인 RECORD를 가져오려면
```
SELECT * FROM (
  SELECT COL1, COL2, COL3, COL4
        , ROW_NUMBERS() OVER ([PARTITION BY COL1] ORDER BY COL4 DESC) AS RN
  FROM TABLE
) WHERE RN = 1;
```
만약 COL4에 NULL값이 나온다면 ORDER BY COL4 에서 NULL이 먼저 나와서 일 수 있다.

`, ROW_NUMBERS() OVER (PARTITION BY COL1 ORDER BY COL4 DESC NULLS LAST) AS RN`**NULLS LAST** 추가
