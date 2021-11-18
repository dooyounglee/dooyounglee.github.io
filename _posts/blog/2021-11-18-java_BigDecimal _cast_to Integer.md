---
layout: post
title: "[java] java.math.BigDecimal cannot be cast to java.lang.Integer"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-11-18T22:40:00-04:00
modified: 2021-11-18T22:40:00-04:00
---

# java java.math.BigDecimal cannot be cast to java.lang.Integer
oracle에서 number값이 Map<String,Object>의 value값일때 Integer.parseInt()에서 형 변환 오류

`int num = Integer.parseInt(map.get("key"));`

## 해결
`int num = Integer.parseInt(String.valueOf(map.get("key")));`
