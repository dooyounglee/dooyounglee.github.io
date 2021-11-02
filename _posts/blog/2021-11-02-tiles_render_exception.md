---
layout: post
title: "[tiles]org.apache.tiles.impl.CannotRenderException 해결"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-11-02T23:14:00-04:00
modified: 2016-06-01T14:19:19-04:00
---

# tiles org.apache.tiles.impl.CannotRenderException
jsp내 tiles 태그에 attribute에 아무런 값이 없을 때 Runtime Exception이 발생

## 해결
```
//file.jsp
<tiles:insertAttribute name="head"/>
```
ignore 기본값은 false
```
<tiles:insertAttribute name="head" ignore="true"/>
```
