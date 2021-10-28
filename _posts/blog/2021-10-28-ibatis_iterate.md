---
layout: post
title: "ibatis iterate"
modified:
categories: blog
excerpt:
tags: []
image:
feature:
date: 2021-10-28T23:14:00-04:00
modified: 2016-06-01T14:19:19-04:00
---

# ibatis iterate
배열 원소들로 IN절 (~,~,...)을 채워서 조회할 때

## Controller.java
```
//배열 원소가 String일때----------
String[] arr1 = request.getParameterValues("name");
Map<String, Object> map = new HashMap<String, Object>();
map.put("key",arr1);
//--------------------------------

//배열 원소가 Map일때----------
List list = new ArrayList();
Map<String, Object> map1 = new HashMap<String, Object>();
map1.put("A","a1");
map1.put("B","b1");
list.add(map1);

Map<String, Object> map2 = new HashMap<String, Object>();
map2.put("A","a2");
map2.put("B","b2");
list.add(map2);

Map<String, Object> map = new HashMap<String, Object>();
map.put("key",list);
//------------------------------
```
## DAO.xml
```
<select id="id" parameterClass="java.util.Map" resultMap="java.util.Map">
SELECT * FROM TABLE
WHERE COL
  <iterate property="key" prepend="IN" open="(" close=")" conjunction=",">
    #key[]#
  </iterate>
</select>
<!-- 실행쿼리
SELECT * FROM TABLE WHERE COL IN (~,~,..)
-->

<select id="id" parameterClass="java.util.Map" resultMap="java.util.Map">
SELECT * FROM TABLE
WHERE 1=1 
  AND (
  <iterate property="key" conjunction="OR">
    (COL1 = #key[].A# AND COL2 = #key[].B#)
  </iterate>
  )
</select>
<!-- 실행쿼리
SELECT * FROM TABLE
WHERE 1=1
AND ((COL1 = 'a1' AND COL2 = 'b1') OR (COL1 = 'a2' AND COL2 = 'b2'));
-->
```


IN절을 다중컬럼 비교로 하고 싶었다.
`WHERE (COL1,COL2) IN (SELECT COL1, COL2 FROM TABLE)` 처럼 서브쿼리로 만들어야 한댄다. 다음처럼 쓸 수도 있다.
```
  WHERE (COL1, COL2)
  <iterate property="key" prepend="IN" open="(" close=")" conjunction="UNION">
    SELECT #key[].A#, #key[].B# FROM DUAL
  </iterate>
  )
```
