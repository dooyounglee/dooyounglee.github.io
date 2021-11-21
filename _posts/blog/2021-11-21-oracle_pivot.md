---
layout: post
title: "[oracle] pivot"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-11-21T21:58:00-04:00
modified: 2021-11-21T21:58:00-04:00
---

# oracle PIVOT
부서  1월_평균 1월_합계 2월_평균 2월_합계 3월_평균 4월_합계 ...

부서1.....1.......2........3........4........5........6

부서2.....1.......2........3........4........5........6

부서3.....1.......2........3........4........5........6

## 방법
```
SELECT 부서, 값, 월 FROM TABLE
PIVOT (AVG(값) AS "평균", SUM(값) AS "합계"
  FOR 월 IN ('01' AS "1월", '02' AS "2월", ..., '12' AS "12월")
)
;
```

## 특정기간 동안 월별 조회
```
SELECT 부서, 값, TO_CHAR(날짜,'MM') AS "월" FROM TABLE
WHERE TO_CHAR(날짜,'YYYYMM') BETWEEN '201001' AND '201806'
PIVOT (AVG(값) AS "평균", SUM(값) AS "합계"
  FOR 월 IN ('01' AS "1월", '02' AS "2월", ..., '12' AS "12월")
);
```
