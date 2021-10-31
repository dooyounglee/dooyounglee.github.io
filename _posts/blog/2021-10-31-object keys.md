---
layout: post
title: "[javascript]object keys 다루기"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-10-31T21:00:00-04:00
modified: 2016-06-01T14:19:19-04:00
---

# javascript object keys
object의 key값들

```
let obj = {};
...
for(let key in obj){ //key: obj의 key
  console.log(obj[key]); //key값의 value출력
}

let arr = Object.keys(obj); //key값들의 arr
arr.length; //key값들의 갯수. obj의 property의 갯수
```
