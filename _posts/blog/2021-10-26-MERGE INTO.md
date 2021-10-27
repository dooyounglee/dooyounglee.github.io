---
layout: post
title: "MERGE INTO"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-10-26T23:31:00-04:00
modified: 2016-06-01T14:19:19-04:00
---

## 오라클 MERGE INTO
```
MERGE INTO TABLE_A A --작업할 테이블
USING TABLE_B B ON (A.COL1 = B.COL1) --조건
WHEN MATCHED THEN --조건에 맞는 경우가 있을 경우
  UPDATE SET A.COL2 = B.COL2
  [WHERE A.COL1 = '123']
WHEN NOT MATCHED THEN --조건에 맞는경우가 없을 경우
  INSERT (A.COL3, A.COL4, A.COL5)
  VALUES (B.COL3, B.COL4, B.COL5)
;
```

- USING절 테이블 자리에 DUAL이 올수도 있다.

- 오라클 10g부터 UPDATE, DELETE, WHERE절 가능

```
MERGE INTO TABLE_A A
USING DUAL
ON (A.COL1 = '123')
WHEN MATCHED THEN
  DELETE --모든 레코드 DELETE
;
```

- ON조건절에 사용된 컬럼을 UPDATE치면 오류난다고 함
